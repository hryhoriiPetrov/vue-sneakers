<script setup>
import CatalogCard from './catalog-card.vue'

defineProps({
  items: Array,
})
</script>

<template>
  <ul class="cards">
    <li v-for="item in items" :key="item.id">
      <catalog-card :title="item.title" :imageUrl="item.imageUrl" :price="item.price" />
    </li>
  </ul>
</template>

<style scoped>
.cards {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  list-style: none;
  padding: 0;
  margin: 0;
}
</style>
