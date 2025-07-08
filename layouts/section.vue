<template>
  <div class="slidev-layout section w-full h-full grid">
    <img
      v-if="$slidev.nav.currentLayout === 'section'"
      v-motion
      :initial="{ x: 200 }"
      :enter="{ x: 30 }"
      src="/cover-back.png"
      class="absolute top-0 right-0 h-full"
      style="filter: grayscale(20%)"
    />
    <Nustar fill="#dddddd" class="absolute right-2 bottom-2 h-22" />
    <div class="my-auto">
      <slot />
    </div>
  </div>
</template>
<script lang="ts" setup>
import Nustar from "../components/Nustar.vue";
</script>