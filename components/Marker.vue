<template>
  <div class="flex items-center gap-2 text-lg">
    <v-icon :icon="icon" size="24" />
    <slot />
  </div>
  <span
    class="bg-$prism-background px-2 py-1 rounded font-mono inline-block text-0.4em transform translate-y-[-1.5em] translate-x-[-0.3em]"
    ><slot
  /></span>
</template>
<script lang="ts" setup>
defineProps({
  icon: {
    type: String,
    default: 'mdi-checkbox-marked-circle'
  }
})
</script>