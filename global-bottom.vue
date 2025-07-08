<template>
  <footer
    v-if="$nav.currentLayout !== 'cover'"
    class="absolute bottom-0 left-0 right-0 p-2"
  >
    <div class="w-full flex justify-between items-center px-4 py-2 text-sm text-gray-500">
      <span>{{ $page + 1 }} / {{ total }}</span>
      <span class="font-semibold">Vitify Admin</span>
    </div>
    <!-- <img class="absolute right-2 bottom-2 h-6" src="/nustar.svg" /> -->
    <Nustar fill="#363636" class="absolute right-2 bottom-2 h-22" />
  </footer>
</template>
<script setup>
import Nustar from "./components/Nustar.vue";
import { useSlideContext } from '@slidev/client'
const { $slidev, $nav ,$page, total } = useSlideContext()
</script>