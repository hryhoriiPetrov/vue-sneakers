<script setup>
import DrawerHeader from './drawer-header.vue'
import DrawerProducts from './drawer-products.vue'
import DrawerFooter from './drawer-footer.vue'
</script>

<template>
  <div class="drawer-bg" />
  <div class="drawer">
    <drawer-header />
    <drawer-products />
    <drawer-footer />
  </div>
</template>

<style scoped>
.drawer-bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0 0 0 / 50%);
}
.drawer {
  position: fixed;
  top: 0;
  bottom: 0;
  right: 0;
  height: 100%;
  width: 100%;
  max-width: 385px;
  background-color: var(--color-white);
  padding: 30px;
  display: flex;
  flex-direction: column;
  gap: 30px;
}
</style>
