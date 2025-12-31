<script setup lang="ts">
import { ref } from 'vue'

const confetti = ref<{ trigger: () => void } | null>(null)

function triggerConfetti() {
  confetti.value?.trigger()
}
</script>

<template>
  <div>
    <UContainer>
      <div class="py-12">
        <UCard>
          <template #header>
            <h1 class="text-2xl font-bold">Welcome to Nuxt UI Layer</h1>
          </template>

          <div class="space-y-4">
            <UAlert
              icon="i-heroicons-information-circle"
              color="primary"
              variant="soft"
              title="Getting Started"
              description="This is a simple page layout using Nuxt UI components."
            />

            <div class="prose dark:prose-invert">
              <p>
                This page demonstrates various Nuxt UI components including:
              </p>
              <ul>
                <li>Container for layout</li>
                <li>Card for content organization</li>
                <li>Alert for notifications</li>
                <li>Button for interactions</li>
                <li>Confetti for celebrations</li>
              </ul>
            </div>

            <div class="flex gap-4">
              <UButton color="primary" size="lg">
                Primary Button
              </UButton>
              <UButton color="gray" variant="soft" size="lg">
                Secondary Button
              </UButton>
              <UButton color="green" size="lg" @click="triggerConfetti">
                🎉 Trigger Confetti
              </UButton>
            </div>
          </div>

          <template #footer>
            <div class="text-sm text-gray-500 dark:text-gray-400">
              Built with Nuxt UI Layer
            </div>
          </template>
        </UCard>
      </div>
    </UContainer>

    <ConfettiAnimation ref="confetti" />
  </div>
</template>
