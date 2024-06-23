<script setup>
import axios from 'axios'
import { ref, provide, reactive, computed, watch, onMounted } from 'vue'

import MainHeader from './components/main/main-header.vue'
import Catalog from './components/catalog/catalog.vue'
import drawer from './components/drawer/drawer.vue'

const drawerOpen = ref(false)
const items = ref([])
const cartItems = ref([])
const totalPrice = computed(calculateTotalPrice)
const vatPrice = computed(calculateVatPrice)
const filters = reactive({
  sortBy: 'title',
  searchQuery: '',
})

function calculateTotalPrice() {
  return cartItems.value.reduce((acc, item) => acc + item.price, 0)
}

function calculateVatPrice() {
  return Math.round((totalPrice.value * 5) / 100)
}

function addToCart(item) {
  cartItems.value.push(item)
  item.isAdded = true
}

function removeFromCart(item) {
  cartItems.value.splice(cartItems.value.indexOf(item), 1)
  item.isAdded = false
}

function onClickAddToCart(item) {
  if (!item.isAdded) {
    addToCart(item)
  } else {
    removeFromCart(item)
  }
}

async function createOrder() {
  try {
    const order = {
      items: cartItems.value,
      totalPrice: totalPrice.value,
    }
    const { data } = await axios.post('https://a7a1da873da050ec.mokky.dev/orders', order)

    cartItems.value = []

    return data
  } catch (error) {
    console.log(error)
  }
}

async function fetchItems() {
  try {
    const params = {
      sortBy: filters.sortBy,
    }

    if (filters.searchQuery) params.title = `*${filters.searchQuery}*`

    const { data } = await axios.get('https://a7a1da873da050ec.mokky.dev/items', {
      params,
    })
    items.value = data.map((item) => ({
      ...item,
      isFavorite: false,
      favoriteId: null,
      isAdded: false,
    }))
  } catch (error) {
    console.error(error)
  }
}

async function fetchFavorites() {
  try {
    const { data } = await axios.get('https://a7a1da873da050ec.mokky.dev/favorites')
    items.value = items.value.map((item) => {
      const favorite = data.find((favorite) => favorite.parentId === item.id)

      if (!favorite) return item

      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id,
      }
    })
    console.log(items.value)
  } catch (error) {
    console.error(error)
  }
}

function onChangeSelect(event) {
  filters.sortBy = event.target.value
}

function onChangeInput(event) {
  filters.searchQuery = event.target.value
}

async function addFavorite(item) {
  try {
    if (!item.isFavorite) {
      const requestObj = {
        ...item,
        parentId: item.id,
      }

      const { data } = await axios.post('https://a7a1da873da050ec.mokky.dev/favorites', requestObj)
      item.isFavorite = true
      item.favoriteId = data.id
      console.log('response', data)
    } else {
      await axios.delete(`https://a7a1da873da050ec.mokky.dev/favorites/${item.favoriteId}`)
      item.isFavorite = false
      item.favoriteId = null
    }
  } catch (error) {
    console.error(error)
  }
}

function openDrawer() {
  drawerOpen.value = true
}

function closeDrawer() {
  drawerOpen.value = false
}

provide('drawerActions', {
  openDrawer,
  closeDrawer,
  removeFromCart,
  onClickAddToCart,
  cartItems,
  totalPrice,
  vatPrice,
  createOrder,
})
provide('catalogActions', {
  items,
  filters,
  fetchItems,
  fetchFavorites,
  onChangeSelect,
  onChangeInput,
  addFavorite,
  onClickAddToCart,
})

onMounted(async () => {
  const localCartItems = localStorage.getItem('cartItems')
  cartItems.value = localCartItems ? JSON.parse(localCartItems) : []

  await fetchItems()
  await fetchFavorites()

  items.value = items.value.map((item) => ({
    ...item,
    isAdded: cartItems.value.some((cartItem) => cartItem.id === item.id),
  }))
})

watch(filters, fetchItems)

watch(cartItems, () => {
  items.value = items.value.map((item) => ({
    ...item,
    isAdded: false,
  }))
})

watch(
  cartItems,
  () => {
    localStorage.setItem('cartItems', JSON.stringify(cartItems.value))
  },
  {
    deep: true,
  }
)
</script>

<template>
  <main-header />
  <catalog />
  <drawer v-if="drawerOpen" />
</template>
