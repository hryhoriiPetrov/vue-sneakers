<script setup>
import DrawerProduct from './drawer-product.vue'
</script>

<template>
  <div class="drawer__products">
    <ul class="drawer__list">
      <li class="drawer__item">
        <drawer-product />
      </li>
      <li class="drawer__item">
        <drawer-product />
      </li>
      <li class="drawer__item">
        <drawer-product />
      </li>
    </ul>
  </div>
</template>

<style scoped>
.drawer__list {
  margin: 0;
  padding: 0;
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-height: 400px;
  overflow-y: scroll;
}
</style>
