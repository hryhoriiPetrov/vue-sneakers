<script setup>
import { inject } from 'vue'
import DrawerProduct from './drawer-product.vue'

const { cartItems, removeFromCart } = inject('drawerActions')
</script>

<template>
  <div class="drawer__products">
    <ul class="drawer__list" v-auto-animate>
      <li class="drawer__item" v-for="cartItem in cartItems" v-bind:key="cartItem.id">
        <drawer-product
          :title="cartItem.title"
          :image-url="cartItem.imageUrl"
          :price="cartItem.price"
          :remove-from-cart="() => removeFromCart(cartItem)"
        />
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
