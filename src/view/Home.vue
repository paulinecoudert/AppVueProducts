<template>
  <div class="home">
    <CategorieBar :categories="categories" @changeCategory="changeCategory" />
    <div class="home__wrapper__products">
      <RouterLink v-for="product in products" :to="`/product/${product.id}`">
        <ProductCard :image="product.image">
          <template #image> {{ product.image }} </template>
          <template #title> {{ product.title }} </template>
          <template #price> {{ product.price }} € </template>
        </ProductCard>
      </RouterLink>
    </div>
  </div>
</template>

<script setup>
import CategorieBar from "../components/CategorieBar.vue";
import ProductCard from "../components/ProductCard.vue";
import { onMounted, ref } from "vue";

const products = ref();
const categories = ref();

onMounted(() => {
  getProducts();
  getCategories();
});

async function getProducts() {
  products.value = await getApi("products");
}

async function getCategories() {
  categories.value = await getApi("products/categories");
}

function getApi(endPoint) {
  return fetch(`https://fakestoreapi.com/${endPoint}`)
    .then((response) => response.json())
    .then((data) => {
      //retourne les valeurs de là où on l'appelle
      return data;
    });
}

// on attend que la valeur revienne de l'Api
async function changeCategory(payload) {
  if (payload === "All") {
    console.log(payload);
    products.value = await getApi("products");
  } else {
    // console.log(await getApi(`category/${payload}`));
    products.value = await getApi(`products/category/${payload}`);
  }
}
</script>

<style>
.home {
  /*  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap; */
}

.home__wrapper__products {
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
</style>
