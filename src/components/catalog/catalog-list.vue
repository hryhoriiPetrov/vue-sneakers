<script setup>
import CatalogCard from './catalog-card.vue'

defineProps({
  items: Array,
})

const emit = defineEmits(['addFavorite'])
</script>

<template>
  <ul class="cards">
    <li v-for="item in items" :key="item.id">
      <catalog-card
        :id="item.id"
        :title="item.title"
        :imageUrl="item.imageUrl"
        :price="item.price"
        :isFavorite="item.isFavorite"
        :onClickFavorite="() => emit('addFavorite', item)"
      />
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
