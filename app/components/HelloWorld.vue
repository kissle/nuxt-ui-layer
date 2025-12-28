<script setup lang="ts">
const { myLayer } = useAppConfig()
</script>

<template>
  <UCard>
    <template #header>
      <h2 class="text-xl font-semibold">Hello World!</h2>
    </template>
    
    <UAlert
      color="success"
      variant="soft"
      title="Layer Configuration"
      :description="`Name: ${myLayer.name}`"
    />
  </UCard>
</template>
