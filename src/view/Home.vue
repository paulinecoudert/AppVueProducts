<template>
  <div class="home">
    <RouterLink v-for="product in products" :to="`/product/${product.id}`">
      <ProductCard :image="product.image">
        <template #image> {{ product.image }} </template>
        <template #title> {{ product.title }} </template>
        <template #price> {{ product.price }} € </template>
      </ProductCard>
    </RouterLink>
  </div>
</template>

<script setup>
import ProductCard from "../components/ProductCard.vue";
import { onMounted, ref } from "vue";

const products = ref([]);

onMounted(() => {
  fetch("https://fakestoreapi.com/products")
    .then((response) => response.json())
    .then((data) => {
      products.value = data;
    });
});
</script>

<style>
.home {
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
</style>
