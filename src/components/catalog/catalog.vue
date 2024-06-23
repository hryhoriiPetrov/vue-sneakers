<script setup>
import CatalogHead from './catalog-head.vue'
import CatalogList from './catalog-list.vue'
</script>

<template>
  <section class="catalog">
    <div class="container">
      <catalog-head />
      <catalog-list />
    </div>
  </section>
</template>

<style scoped>
.catalog {
  padding: 40px 0;
}
</style>
