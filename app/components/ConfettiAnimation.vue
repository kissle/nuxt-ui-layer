<script setup lang="ts">
import { ref, onMounted, onUnmounted, watch } from 'vue'

interface ConfettiParticle {
  x: number
  y: number
  vx: number
  vy: number
  color: string
  rotation: number
  rotationSpeed: number
  width: number
  height: number
  active: boolean
}

const props = defineProps<{
  show?: boolean
}>()

const emit = defineEmits<{
  complete: []
}>()

const canvas = ref<HTMLCanvasElement | null>(null)
let ctx: CanvasRenderingContext2D | null = null
let particles: ConfettiParticle[] = []
let animationId: number | null = null
let isAnimating = false

const colors = ['#ff0000', '#00ff00', '#0000ff', '#ffff00', '#ff00ff', '#00ffff', '#ffa500', '#ff1493']

function createParticles() {
  particles = []
  const particleCount = 150
  
  for (let i = 0; i < particleCount; i++) {
    particles.push({
      x: Math.random() * (canvas.value?.width || 0),
      y: -20,
      vx: (Math.random() - 0.5) * 10,
      vy: Math.random() * 5 + 2,
      color: colors[Math.floor(Math.random() * colors.length)],
      rotation: Math.random() * 360,
      rotationSpeed: (Math.random() - 0.5) * 10,
      width: Math.random() * 10 + 5,
      height: Math.random() * 8 + 4,
      active: true
    })
  }
}

function updateParticles() {
  let activeCount = 0
  
  particles.forEach(particle => {
    if (!particle.active) return
    
    particle.x += particle.vx
    particle.y += particle.vy
    particle.vy += 0.3 // gravity
    particle.rotation += particle.rotationSpeed
    
    // Mark particle as inactive if off screen
    if (particle.y > (canvas.value?.height || 0) + 20) {
      particle.active = false
    } else {
      activeCount++
    }
  })
  
  if (activeCount === 0 && isAnimating) {
    stopAnimation()
    emit('complete')
  }
}

function drawParticles() {
  if (!ctx || !canvas.value) return
  
  ctx.clearRect(0, 0, canvas.value.width, canvas.value.height)
  
  particles.forEach(particle => {
    if (!particle.active) return
    
    ctx.save()
    ctx.translate(particle.x, particle.y)
    ctx.rotate((particle.rotation * Math.PI) / 180)
    ctx.fillStyle = particle.color
    ctx.fillRect(-particle.width / 2, -particle.height / 2, particle.width, particle.height)
    ctx.restore()
  })
}

function animate() {
  if (!isAnimating) return
  
  updateParticles()
  drawParticles()
  
  animationId = requestAnimationFrame(animate)
}

function startConfetti() {
  if (isAnimating) return
  
  if (!canvas.value) return
  
  canvas.value.width = window.innerWidth
  canvas.value.height = window.innerHeight
  
  createParticles()
  isAnimating = true
  animate()
}

function stopAnimation() {
  isAnimating = false
  if (animationId !== null) {
    cancelAnimationFrame(animationId)
    animationId = null
  }
}

function handleResize() {
  if (canvas.value) {
    canvas.value.width = window.innerWidth
    canvas.value.height = window.innerHeight
  }
}

onMounted(() => {
  if (canvas.value) {
    ctx = canvas.value.getContext('2d')
    canvas.value.width = window.innerWidth
    canvas.value.height = window.innerHeight
  }
  
  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  stopAnimation()
  window.removeEventListener('resize', handleResize)
})

watch(() => props.show, (newValue) => {
  if (newValue) {
    startConfetti()
  } else {
    stopAnimation()
  }
})

// Expose method to trigger confetti programmatically
defineExpose({
  trigger: startConfetti
})
</script>

<template>
  <canvas
    ref="canvas"
    class="fixed inset-0 pointer-events-none z-50"
  />
</template>
