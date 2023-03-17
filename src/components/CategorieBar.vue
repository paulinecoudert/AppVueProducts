<template>
  <div id="CategorieBar" v-if="categories && categories.length > 0">
    <p
      :class="{ actualCategory: actualCategory === 'All' }"
      @click="changeCategory('All')"
    >
      All
    </p>
    <p
      :class="{ actualCategory: actualCategory === categorie }"
      v-for="(categorie, index) in categories"
      :key="index"
      @click="changeCategory(categorie)"
    >
      {{ categorie }}
    </p>
  </div>
</template>

<script setup>
import { defineProps, defineEmits, ref } from "vue";
const actualCategory = ref("All");
const props = defineProps({
  categories: {
    required: true,
    type: Array,
  },
});

const event = defineEmits("changeCategory");

// creation d'un event qu'on veut émettre
function changeCategory(categorie) {
  event("changeCategory", categorie);
  actualCategory.value = categorie;
}
</script>

// 'scoped' ne déborde pas
<style scoped>
#CategorieBar {
  margin: auto;
  display: flex;
  max-width: 400px;
  align-items: center;
  justify-content: space-between;
  cursor: pointer;
}

.actualCategory {
  text-decoration: underline;
}
</style>
