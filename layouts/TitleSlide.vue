<template>
  <div class="h-full flex flex-col justify-center items-center text-center">
    <h1 class="text-5xl font-bold text-primary mb-4">
      {{ title }}
    </h1>
    <p class="text-md text-gray-500">{{ subtitle }}</p>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  subtitle: String,
})
</script>