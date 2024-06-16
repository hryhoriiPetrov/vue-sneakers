<script setup>
import axios from 'axios'
import { onMounted, ref } from 'vue'

import CatalogHead from './catalog-head.vue'
import CatalogList from './catalog-list.vue'

const items = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get('https://a7a1da873da050ec.mokky.dev/items')
    items.value = data
  } catch (error) {
    console.error(error)
  }
})
</script>

<template>
  <section class="catalog">
    <div class="container">
      <catalog-head />
      <catalog-list :items="items" />
    </div>
  </section>
</template>

<style scoped>
.catalog {
  padding: 40px 0;
}
</style>
