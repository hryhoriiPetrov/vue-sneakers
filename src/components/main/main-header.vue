<script setup>
import { inject } from 'vue'

import IconCart from '../icons/icon-cart.vue'
import IconHeart from '../icons/icon-heart.vue'
import IconProfile from '../icons/icon-profile.vue'

const { openDrawer, totalPrice } = inject('drawerActions')
</script>

<template>
  <header class="header">
    <div class="container header__container">
      <a class="logo" href="/">
        <img class="logo__img" src="/images/logo.png" alt="Vue Sneakers Логотип" />
        <div class="logo__sign">
          <span class="logo__title">Vue Sneakers</span>
          <span class="logo__subtitle">Магазин лучших кроссовок</span>
        </div>
      </a>
      <nav class="nav">
        <ul class="nav__list">
          <li class="nav__item">
            <button
              class="nav__btn"
              type="button"
              aria-label="Кнопка для открытия корзины"
              v-on:click="openDrawer"
            >
              <icon-cart />
              <span>{{ totalPrice }} руб.</span>
            </button>
          </li>
          <li class="nav__item">
            <a class="nav__link" href="/">
              <icon-heart />
              <span>Закладки</span>
            </a>
          </li>
          <li class="nav__item">
            <a class="nav__link" href="/">
              <icon-profile />
              <span>Профиль</span>
            </a>
          </li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<style scoped>
.header {
  padding: 43px 0;
  border-bottom: 1px solid var(--color-gallery);
}
.header__container {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.logo {
  display: flex;
  gap: 16px;
  color: inherit;
  text-decoration: none;
  transition: transform 0.1s ease-in-out;
}
.logo:hover {
  transform: translateY(-2px);
}
.logo__img {
  width: 40px;
  height: 40px;
  object-fit: contain;
  border-radius: 100%;
}
.logo__title,
.logo__subtitle {
  display: block;
}
.logo__title {
  font-weight: 700;
  font-size: 20px;
  text-transform: uppercase;
}
.logo__subtitle {
  color: var(--color-silver-chalice);
}
.nav__list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  align-items: center;
  gap: 32px;
}
.nav__link,
.nav__btn {
  text-decoration: none;
  color: var(--color-scorpion);
  display: flex;
  align-items: center;
  gap: 8px;
}
.nav__link svg,
.nav__btn svg {
  width: 18px;
  height: 18px;
}
.nav__btn {
  border: none;
  background-color: transparent;
  padding: 0;
  cursor: pointer;
}
.nav__link:hover {
  text-decoration: underline;
}
</style>
