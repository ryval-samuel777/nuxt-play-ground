<template>
  <div>
    <div>
      <p>{{ product.title }}</p>
      <p>{{ product.price }}</p>
      <p>{{ product.description }}</p>
      <p>{{ product.category }}</p>
    </div>
  </div>
</template>

<script setup>
const route = useRoute();
const uri = `https://fakestoreapi.com/products/` + id;

const { data: product } = await useFetch(uri, {key: id});

definePageMeta({
    layaout: 'products',
})

</script>
