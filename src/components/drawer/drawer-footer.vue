<script setup>
import IconArrowWhite from '../icons/icon-arrow-white.vue'
</script>

<template>
  <div class="drawer__footer">
    <ul class="drawer__list">
      <li class="drawer__item">
        <span class="drawer__detail">Итого:</span>
        <span class="drawer__price">21 498 руб.</span>
      </li>
      <li class="drawer__item">
        <span class="drawer__detail">Налог 5%:</span>
        <span class="drawer__price">1074 руб.</span>
      </li>
    </ul>
    <button class="drawer__buy" type="button">
      <span>Оформить заказ</span>
      <icon-arrow-white />
    </button>
  </div>
</template>

<style scoped>
.drawer__footer {
  margin-top: auto;
}
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
.drawer__item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 16px;
}
.drawer__price {
  font-weight: 700;
}
.drawer__buy {
  border: none;
  background-color: var(--color-conifer);
  padding: 18px 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  border-radius: 18px;
  font-weight: 600;
  font-size: 16px;
  color: var(--color-white);
  margin-top: 24px;
  width: 100%;
  cursor: pointer;
}
.drawer__buy:disabled {
  background-color: var(--color-scorpion);
  cursor: not-allowed;
}
</style>
