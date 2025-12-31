# ConfettiAnimation Component

A simple, lightweight confetti animation component for Vue 3 / Nuxt applications. This component uses native JavaScript and the Canvas API to create a colorful confetti effect without requiring any additional packages.

## Features

- ✨ Pure JavaScript implementation (no dependencies)
- 🎨 Colorful confetti particles with realistic physics
- 🎯 Can be triggered programmatically or via props
- 🔄 Auto-cleanup when animation completes
- 📱 Responsive - adapts to window resize
- ⚡ Lightweight and performant with optimized particle management

## Usage

### Basic Usage (Programmatic)

```vue
<script setup>
import { ref } from 'vue'

const confetti = ref(null)

function celebrate() {
  confetti.value?.trigger()
}
</script>

<template>
  <div>
    <button @click="celebrate">Celebrate! 🎉</button>
    <ConfettiAnimation ref="confetti" />
  </div>
</template>
```

### Using Props

```vue
<script setup>
import { ref } from 'vue'

const showConfetti = ref(false)

function celebrate() {
  showConfetti.value = true
}
</script>

<template>
  <div>
    <button @click="celebrate">Celebrate! 🎉</button>
    <ConfettiAnimation :show="showConfetti" @complete="showConfetti = false" />
  </div>
</template>
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `show` | `boolean` | `undefined` | When set to `true`, triggers the confetti animation |

## Events

| Event | Description |
|-------|-------------|
| `complete` | Emitted when the confetti animation completes (all particles have fallen off screen) |

## Exposed Methods

The component exposes the following methods via template refs:

| Method | Description |
|--------|-------------|
| `trigger()` | Manually trigger the confetti animation |

## How It Works

The component creates 150 colorful confetti particles that:
- Start from the top of the screen at random X positions
- Fall with gravity simulation
- Rotate as they fall for added realism
- Have random colors, sizes, and velocities
- Are marked as inactive when off-screen (optimized for performance)
- Automatically clean up when all particles are inactive

## Performance Optimizations

- Uses an `active` flag instead of filtering arrays every frame to reduce garbage collection
- Context null checks are done outside loops for better performance
- Particles are reused in the array instead of being recreated

## Customization

If you need to customize the confetti (colors, particle count, physics, etc.), you can modify the component directly:

- **Colors**: Edit the `colors` array (line 29)
- **Particle Count**: Change `particleCount` in `createParticles()` (line 33)
- **Gravity**: Adjust the gravity value in `updateParticles()` (line 58)
- **Velocities**: Modify the `vx` and `vy` values in `createParticles()` (lines 40-41)

## Browser Support

This component works in all modern browsers that support:
- Canvas API
- ES6+ JavaScript
- Vue 3

## License

This component is part of the nuxt-ui-layer project.
