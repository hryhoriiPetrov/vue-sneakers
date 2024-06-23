<script setup>
import { inject } from 'vue'
import IconSearch from '../icons/icon-search.vue'

const { onChangeInput, onChangeSelect } = inject('catalogActions')
</script>

<template>
  <div class="catalog__head">
    <h2 class="title catalog__title">Все кроссовки</h2>
    <div class="catalog__filters">
      <select class="catalog__sort" @change="onChangeSelect">
        <option value="name">По названию</option>
        <option value="price">По цене (дешевые)</option>
        <option value="-price">По цене (дорогие)</option>
      </select>
      <div class="catalog__search">
        <icon-search />
        <input class="catalog__input" type="text" placeholder="Поиск..." @input="onChangeInput" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.catalog__head {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 40px;
}
.catalog__filters {
  display: flex;
  align-items: center;
  gap: 12px;
}
.catalog__sort {
  border: 1px solid var(--color-concrete);
  border-radius: 10px;
  padding: 15px;
  font-size: 14px;
  color: var(--color-silver);
  outline-color: var(--color-silver-chalice);
  outline-width: 1px;
  appearance: none;
  text-align: center;
}
.catalog__search {
  position: relative;
}
.catalog__search svg {
  position: absolute;
  top: 15px;
  left: 18px;
  width: 15px;
  height: 15px;
}
.catalog__input {
  border: 1px solid var(--color-concrete);
  border-radius: 10px;
  padding: 15px 18px 15px 46px;
  font-size: 14px;
  color: var(--color-silver);
  outline-color: var(--color-silver-chalice);
  outline-width: 1px;
}
.catalog__input::placeholder {
  color: var(--color-silver);
}
</style>
