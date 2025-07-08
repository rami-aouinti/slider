<template>
  <div class="border rounded p-4 bg-white dark:bg-gray-900">
    <h3 class="text-xl font-semibold mb-1">{{ title }}</h3>
    <p class="text-gray-600 dark:text-gray-400">{{ description }}</p>
  </div>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    viewBox="0 0 400 200"
    class="svg"
  >
    <defs>
      <g id="vue">
        <path
          fill="#4dba87"
          d="M 0,0 -22.669,39.264 -45.338,0 h -75.491 L -22.669,170.017 75.491,0 Z"
        ></path>
        <path
          fill="#435466"
          d="M 0,0 -22.669,39.264 -45.338,0 H -81.565 L -22.669,102.01 36.227,0 Z"
        ></path>
      </g>
      <clipPath id="cut1">
        <rect x="0" y="0" width="150" height="200"></rect>
      </clipPath>
      <clipPath id="cut2">
        <rect x="250" y="0" width="150" height="200"></rect>
      </clipPath>
    </defs>
    <g clip-path="url(#cut1)">
      <g class="anim">
        <use transform="translate(173, 30)" xlink:href="#vue"></use>
      </g>
    </g>
    <g clip-path="url(#cut2)">
      <g class="anim">
        <use transform="translate(273, 30)" xlink:href="#vue"></use>
      </g>
    </g>
    <line x1="150" y1="20" x2="150" y2="200" stroke="#579BDD"></line>
    <line x1="250" y1="20" x2="250" y2="200" stroke="#DA9022"></line>
  </svg>
</template>
<script lang="ts" setup>
defineProps({
  title: String,
  description: String,
})
</script>
<style>
.anim {
  transform-origin: 50% 50%;
  animation: anim 1s alternate infinite ease-in-out;
}
@keyframes anim {
  0% {
    transform: translate(-50px) rotate(10deg);
  }
  100% {
    transform: translate(50px) rotate(-10deg);
  }
}
</style>
