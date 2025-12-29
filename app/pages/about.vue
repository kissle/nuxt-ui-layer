<template>
  <div>
    <UContainer>
      <div class="py-12">
        <UCard>
          <template #header>
            <h1 class="text-2xl font-bold">About Page</h1>
          </template>

          <div class="prose dark:prose-invert">
            <p>
              This is a test page to verify that the default layout is applied consistently across all pages.
            </p>
            <p>
              The header and footer should be visible on this page as well, demonstrating that the layout is working correctly.
            </p>
          </div>

          <template #footer>
            <UButton to="/" color="primary">
              Back to Home
            </UButton>
          </template>
        </UCard>
      </div>
    </UContainer>
  </div>
</template>
