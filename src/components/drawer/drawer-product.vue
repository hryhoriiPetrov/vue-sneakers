<script setup>
import IconCross from '../icons/icon-cross.vue'
</script>

<template>
  <div class="drawer-product">
    <img
      class="drawer-product__img"
      src="/public/images/sneakers-1.jpg"
      alt="Мужские Кроссовки Nike Air Max 270"
    />
    <div class="drawer-product__details">
      <span class="drawer-product__title">Мужские Кроссовки Nike Air Max 270</span>
      <span class="drawer-product__price">12 999 руб.</span>
    </div>
    <button class="drawer-product__delete" type="button">
      <icon-cross />
    </button>
  </div>
</template>

<style scoped>
.drawer-product {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  width: 100%;
  padding: 20px;
  border: 1px solid var(--color-concrete);
  border-radius: 20px;
}
.drawer-product__img {
  width: 70px;
  height: 70px;
  object-fit: contain;
}
.drawer-product__details {
  width: 100%;
  max-width: 150px;
}
.drawer-product__delete {
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
.drawer-product__title {
  display: block;
  font-size: 14px;
  margin-bottom: 8px;
}
.drawer-product__price {
  display: block;
  font-weight: 700;
  font-size: 14px;
}
</style>
