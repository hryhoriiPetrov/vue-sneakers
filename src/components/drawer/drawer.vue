<script setup>
import { inject } from 'vue'

import DrawerHeader from './drawer-header.vue'
import DrawerProducts from './drawer-products.vue'
import DrawerFooter from './drawer-footer.vue'
import MainInfo from '../main/main-info.vue'

const { closeDrawer, totalPrice } = inject('drawerActions')
</script>

<template>
  <div class="drawer-bg" v-on:click="closeDrawer" />
  <div class="drawer">
    <drawer-header />
    <div class="drawer__message" v-if="!totalPrice">
      <main-info
        img-url="/images/empty-cart.png"
        title="Корзина пустая"
        subtitle="Добавьте хотя бы одну пару кроссовок, чтобы сделать заказ."
      />
    </div>
    <drawer-products v-if="totalPrice" />
    <drawer-footer v-if="totalPrice" />
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
.drawer__message {
  margin: auto 0;
}
</style>
