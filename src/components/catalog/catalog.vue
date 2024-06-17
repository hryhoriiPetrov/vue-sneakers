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
    items.value = data
  } catch (error) {
    console.error(error)
  }
}

onMounted(fetchItems)
watch(filters, fetchItems)
</script>

<template>
  <section class="catalog">
    <div class="container">
      <catalog-head :onChangeSelect="onChangeSelect" :onChangeInput="onChangeInput" />
      <catalog-list :items="items" />
    </div>
  </section>
</template>

<style scoped>
.catalog {
  padding: 40px 0;
}
</style>
