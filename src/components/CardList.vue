<script setup>
import Card from './Card.vue'

const onClickAdd = () => {}
const onClickFavorite = () => {}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      title="Nike Blazer Mid Suede"
      image-url="/sneakers/sneakers-1.jpg"
      :price="120"
      :on-click-favorite="onClickAdd"
      :on-click-add="onClickFavorite"
    />
  </div>
</template>
