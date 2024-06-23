<script setup>
defineProps({
  imgUrl: String,
  title: String,
  subtitle: String,
})
</script>

<template>
  <div class="info">
    <img class="info__img" :src="imgUrl" :alt="title" />
    <h2 class="info__title">{{ title }}</h2>
    <span class="info__subtitle">{{ subtitle }}</span>
  </div>
</template>

<style scoped>
.info {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}
.info__img {
  width: 120px;
  height: 120px;
  object-fit: contain;
  margin: 0 0 21px;
}
.info__title {
  font-weight: 600;
  font-size: 22px;
  margin: 0 0 9px;
}
.info__subtitle {
  font-size: 16px;
  color: rgba(0 0 0 / 40%);
  margin: 0 0 40px;
}
</style>
