<script setup>
import { onMounted, ref, watch } from 'vue'
import axios from 'axios'

import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
// import Drawer from './components/Drawer.vue'

const items = ref([])
const filters = ref({
  sortBy: 'title',
  searchQuery: ''
})

const onChangeSelect = (event) => {
  filters.value.sortBy = event.target.value
}

const onChangeSearchInput = (event) => {
  filters.value.searchQuery = event.target.value
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(`https://bdbf900dc532c768.mokky.dev/favorites`)

    items.value = items.value.map((item) => {
      const favorite = favorites.find((favorite) => favorite.productId === item.id)

      if (!favorite) {
        return item
      } else {
        return {
          ...item,
          isFavorite: true,
          favoriteId: favorite.id
        }
      }
    })
  } catch (error) {
    console.log(error)
  }
}

const addToFavorite = async (item) => {
  try {
    if (!item.isFavorite) {
      item.isFavorite = true

      const obj = {
        productId: item.id
      }

      const { data } = await axios.post(`https://bdbf900dc532c768.mokky.dev/favorites`, obj)

      item.favoriteId = data.id
    } else {
      item.isFavorite = false
      await axios.delete(`https://bdbf900dc532c768.mokky.dev/favorites/${item.favoriteId}`)
      item.favoriteId = null
    }
  } catch (error) {
    console.log(error)
  }
}

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.value.sortBy
    }

    if (filters.value.searchQuery) {
      params.title = `*${filters.value.searchQuery}*`
    }

    const { data } = await axios.get(`https://bdbf900dc532c768.mokky.dev/items`, { params: params })
    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      favoriteId: null,
      isAdded: false
    }))
  } catch (error) {
    console.log(error)
  }
}

onMounted(async () => {
  await fetchItems()
  await fetchFavorites()
})

watch(filters.value, fetchItems)
</script>

<template>
  <!-- <Drawer /> -->
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header></Header>

    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">All Sneakers</h2>

        <div class="flex gap-4">
          <select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none">
            <option value="name">Name</option>
            <option value="-price">Price (High-Low)</option>
            <option value="price">Price (Low-High)</option>
          </select>

          <div class="relative">
            <img class="absolute left-4 top-3" src="/search.svg" alt="" />
            <input
              @input="onChangeSearchInput"
              class="border rounded-md py-2 pl-11 pr02 outline-none focus:border-gray-400"
              type="text"
              placeholder="Search..."
            />
          </div>
        </div>
      </div>

      <div class="mt-10">
        <CardList :items="items" @addToFavorite="addToFavorite" />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
