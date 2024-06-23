<script setup>
import { inject } from 'vue'
import { useAutoAnimate } from '@formkit/auto-animate/vue'
import CatalogCard from './catalog-card.vue'

const { items, onClickAddToCart, addFavorite } = inject('catalogActions')
const [parent] = useAutoAnimate()
</script>

<template>
  <ul class="cards" ref="parent">
    <li v-for="item in items" :key="item.id">
      <catalog-card
        :id="item.id"
        :title="item.title"
        :imageUrl="item.imageUrl"
        :price="item.price"
        :isFavorite="item.isFavorite"
        :isAdded="item.isAdded"
        :onClickFavorite="() => addFavorite(item)"
        :onClickAdd="() => onClickAddToCart(item)"
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
