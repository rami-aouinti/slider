<template>
  <footer
    v-if="$slidev.nav.currentLayout !== 'cover'"
    class="absolute bottom-0 left-0 right-0 p-2"
  >
    <!-- <img class="absolute right-2 bottom-2 h-6" src="/nustar.svg" /> -->
    <Nustar fill="#363636" class="absolute right-2 bottom-2 h-22" />
  </footer>
</template>
