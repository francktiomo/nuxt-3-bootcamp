<script setup>
const { cars } = useCars();

const favorite = useLocalStorage("favorite", {});

const handleFavorite = (id) => {
  if (id in favorite.value) {
    delete favorite.value[id];
  } else {
    favorite.value = {
      ...favorite.value,
      [id]: true,
    };
  }
};
</script>

<template>
  <div class="w-full">
    <!-- ClientOnly is used to enforce client side rendering on the component it wraps
    It allows the component to access the LocalStorage
    Wrapping the component is one way to do it, anoher way is to rename the component file like thi: ComponentName.client.vue -->
    <ClientOnly>
      <CarCard
        v-for="car in cars"
        :key="car.id"
        :car="car"
        @favor="handleFavorite"
        :favored="car.id in favorite"
      />
    </ClientOnly>
  </div>
</template>
