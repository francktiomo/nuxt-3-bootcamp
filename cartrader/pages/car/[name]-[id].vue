<script setup>
const { toTitleCase } = useUtilities();
const route = useRoute();
const { cars } = useCars();
useHead({
  title: toTitleCase(route.params.name),
});

const car = computed(() => {
  return cars.find((c) => {
    return c.id == parseInt(route.params.id);
  });
});

// Server-side error
if (!car.value) {
  throw createError({
    statusCode: 404,
    message: `Car with ID ${route.params.id} does not exist`,
  });
}

definePageMeta({
  layout: "custom",
});
</script>

<template>
  <div v-if="car">
    <CarDetailHero :car="car" />
    <CarDetailAttributes :features="car.features" />
    <CarDetailDescription :description="car.description" />
    <CarDetailContact />
  </div>
</template>
