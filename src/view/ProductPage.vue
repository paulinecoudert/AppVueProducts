<template>
  <div class="">
    <img :src="product?.image" />
    <h3>{{ product?.title }}</h3>
    <p>{{ product?.description }} €</p>
    <p>{{ product?.price }} €</p>
  </div>
</template>

<script setup>
import { useRoute } from "vue-router";
import { onMounted, ref } from "vue";

const route = useRoute();
const product = ref();

// objet pour récupérer l'identifiant pour récupérer la data exacte ${route.params.id}
onMounted(() => {
  fetch(`https://api.storerestapi.com/products/${route.params.id}`)
    .then((response) => response.json())
    .then((data) => {
      product.value = data;
    });
});
</script>

<style></style>
