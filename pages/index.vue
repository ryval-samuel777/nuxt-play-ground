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
    <!-- <NuxtLayout /> -->

    <NuxtLayout name="default" />
    <h1>
      ini halaman utama
    </h1>
  </div>
</template>
