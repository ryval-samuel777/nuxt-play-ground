<script setup>
import { onMounted } from "vue";
import { initFlowbite } from "flowbite";

// initialize components based on data attribute selectors
onMounted(() => {
  initFlowbite();
});
</script>

<template>
  <div>
    <SideBar />
    <div class="p-4 sm:ml-64"></div>
    <slot />
  </div>
</template>
