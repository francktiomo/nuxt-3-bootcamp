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
      <CarSideBar />
      <NuxtPage />
    </div>
  </div>
</template>
