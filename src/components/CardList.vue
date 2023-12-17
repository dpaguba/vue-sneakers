<script setup>
import Card from './Card.vue'
defineProps({
  items: Array
})

const onClickAdd = () => {}
const onClickFavorite = () => {}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      v-for="item in items"
      :key="item.id"
      :title="item.title"
      :image-url="item.imageUrl"
      :price="item.price"
      :on-click-favorite="onClickAdd"
      :on-click-add="onClickFavorite"
    />
  </div>
</template>
