<script setup>
import { inject } from 'vue'

import IconCross from '../icons/icon-cross.vue'

const { closeDrawer } = inject('drawerActions')
</script>

<template>
  <div class="drawer__header">
    <h2 class="title drawer__title">Корзина</h2>
    <button
      class="drawer__close"
      type="button"
      aria-label="Кнопка для закрытия корзины"
      v-on:click="closeDrawer"
    >
      <icon-cross />
    </button>
  </div>
</template>

<style scoped>
.drawer__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.drawer__close {
  width: 32px;
  height: 32px;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid var(--color-silver);
  border-radius: 8px;
  background-color: transparent;
  cursor: pointer;
}
.drawer__close svg {
  width: 11px;
  height: 11px;
}
</style>
