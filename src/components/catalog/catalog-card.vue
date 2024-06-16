<script setup>
import IconHeartCard from '../icons/icon-heart-card.vue'
import IconPlus from '../icons/icon-plus.vue'
import IconChecked from '../icons/icon-checked.vue'
import IconFavorite from '../icons/icon-favorite.vue'

defineProps({
  title: String,
  imageUrl: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickAdd: Function,
  onClickFavorite: Function,
})
</script>

<template>
  <div class="card">
    <button
      :class="isFavorite ? 'card__favorite card__favorite--added' : 'card__favorite'"
      type="button"
      aria-label="Добавить товар в избранное"
      @click="onClickFavorite"
    >
      <icon-favorite v-if="isFavorite" />
      <icon-heart-card v-else />
    </button>
    <img class="card__img" :src="imageUrl" :alt="title" />
    <span class="card__title">{{ title }}</span>
    <div class="card__footer">
      <div class="card__price">
        <span class="card__label">Цена:</span>
        <span class="card__num">{{ price }} руб.</span>
      </div>
      <button
        :class="isAdded ? 'card__btn card__btn--checked' : 'card__btn'"
        type="button"
        aria-label="Добавить в корзину"
        @click="onClickAdd"
      >
        <icon-checked v-if="isAdded" />
        <icon-plus v-else />
      </button>
    </div>
  </div>
</template>

<style scoped>
.card {
  position: relative;
  padding: 20px 30px;
  border: 1px solid var(--color-concrete);
  border-radius: 40px;
  background-color: var(--color-white);
  transition:
    transform 0.2s ease-in-out,
    box-shadow 0.2s ease-in-out;
}
.card:hover {
  box-shadow: 0 14px 30px 0 rgba(0, 0, 0, 0.05);
  transform: translateY(-5px);
}
.card__favorite {
  position: absolute;
  top: 20px;
  left: 20px;
  background-color: transparent;
  border: 1px solid var(--color-alabaster);
  border-radius: 7px;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 30px;
  height: 30px;
}
.card__favorite svg {
  width: 16px;
  height: 16px;
}
.card__favorite--added {
  background-color: var(--color-bridesmaid);
}
.card__img,
.card__title {
  margin-bottom: 14px;
}
.card__title {
  display: block;
}
.card__footer {
  display: flex;
  justify-content: space-between;
}
.card__price {
  display: flex;
  flex-direction: column;
  gap: 2px;
}
.card__label {
  font-weight: 500;
  font-size: 11px;
  text-transform: uppercase;
  color: var(--color-silver);
}
.card__num {
  font-weight: 700;
}
.card__btn {
  width: 32px;
  height: 32px;
  border: 1px solid var(--color-concrete);
  border-radius: 8px;
  background-color: transparent;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
.card__btn svg {
  width: 11px;
  height: 11px;
}
.card__btn--checked {
  background: linear-gradient(180deg, #89f09c 0%, #3cc755 100%);
  border: none;
}
</style>
