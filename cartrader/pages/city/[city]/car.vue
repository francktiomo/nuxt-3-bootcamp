<script setup>
const { toTitleCase } = useUtilities();
const router = useRoute();
useHead({
  title: `${
    router.params.make ? toTitleCase(router.params.make) : "Cars"
  } in ${toTitleCase(router.params.city)}`,
});

definePageMeta({
  layout: "custom",
});
</script>

<template>
  <div>
    <div class="mt-32 flex">
      <!-- NuxtErrorBoundary: Used to handle client side error -->
      <NuxtErrorBoundary>
        <CarSideBar />
        <NuxtPage />
        <!-- S'affiche lorsqu'une erreur est catchée par NuxtErrorBoundary -->
        <template #error="{ error }">
          <div class="text-center mx-auto flex flex-col">
            <h1 class="text-5xl text-red-600 mb-4">Something went wrong</h1>
            <code>{{ error }}</code>
            <button
              class="text-white bg-blue-400 px-10 py-3 rounded mt-4"
              @click="error.value = null"
            >
              Go back
            </button>
          </div>
        </template>
      </NuxtErrorBoundary>
    </div>
  </div>
</template>
