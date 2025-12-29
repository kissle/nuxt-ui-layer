<template>
  <div>
    <UHeader title="Nuxt UI Layer">
      <template #right>
        <UColorModeButton />
      </template>
    </UHeader>

    <UPage>
      <slot />
    </UPage>

    <UFooter>
      <template #left>
        <p class="text-sm text-gray-500 dark:text-gray-400">
          © {{ new Date().getFullYear() }} Nuxt UI Layer. All rights reserved.
        </p>
      </template>

      <template #right>
        <UButton
          to="https://github.com/kissle/nuxt-ui-layer"
          target="_blank"
          color="gray"
          variant="ghost"
          icon="i-simple-icons-github"
          aria-label="GitHub"
        />
      </template>
    </UFooter>
  </div>
</template>
