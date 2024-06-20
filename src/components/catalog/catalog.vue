<script setup>
import axios from 'axios'
import { onMounted, ref, reactive, watch } from 'vue'

import CatalogHead from './catalog-head.vue'
import CatalogList from './catalog-list.vue'

const items = ref([])
const filters = reactive({
  sortBy: 'title',
  searchQuery: '',
})

function onChangeSelect(event) {
  filters.sortBy = event.target.value
}

function onChangeInput(event) {
  filters.searchQuery = event.target.value
}

async function fetchItems() {
  try {
    const params = {
      sortBy: filters.sortBy,
    }

    if (filters.searchQuery) params.title = `*${filters.searchQuery}*`

    const { data } = await axios.get('https://a7a1da873da050ec.mokky.dev/items', {
      params,
    })
    items.value = data.map((item) => ({
      ...item,
      isFavorite: false,
      favoriteId: null,
      isAdded: false,
    }))
  } catch (error) {
    console.error(error)
  }
}

async function fetchFavorites() {
  try {
    const { data } = await axios.get('https://a7a1da873da050ec.mokky.dev/favorites')
    items.value = items.value.map((item) => {
      const favorite = data.find((favorite) => favorite.parentId === item.id)

      if (!favorite) return item

      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id,
      }
    })
    console.log(items.value)
  } catch (error) {
    console.error(error)
  }
}

async function addFavorite(item) {
  try {
    if (!item.isFavorite) {
      const requestObj = {
        ...item,
        parentId: item.id,
      }

      const { data } = await axios.post('https://a7a1da873da050ec.mokky.dev/favorites', requestObj)
      item.isFavorite = true
      item.favoriteId = data.id
      console.log('response', data)
    } else {
      await axios.delete(`https://a7a1da873da050ec.mokky.dev/favorites/${item.favoriteId}`)
      item.isFavorite = false
      item.favoriteId = null
    }
  } catch (error) {
    console.error(error)
  }
}

onMounted(async () => {
  await fetchItems()
  await fetchFavorites()
})
watch(filters, fetchItems)
</script>

<template>
  <section class="catalog">
    <div class="container">
      <catalog-head :onChangeSelect="onChangeSelect" :onChangeInput="onChangeInput" />
      <catalog-list :items="items" @addFavorite="addFavorite" />
    </div>
  </section>
</template>

<style scoped>
.catalog {
  padding: 40px 0;
}
</style>
