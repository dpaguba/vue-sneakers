<script setup>
defineProps({
  title: String,
  price: Number,
  imageUrl: String,
  isFavorite: Boolean,
  isAdded: Boolean
})
</script>

<template>
  <div
    class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition"
  >
    <img src="/like-2.svg" alt="Like 1" class="absolute top-8 left-8" />
    <img src="/sneakers/sneakers-1.jpg" alt="Sneaker" />
    <p class="mt-2">{{ title }}</p>

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-400">Price:</span>
        <b> {{ price }} $ </b>
      </div>
      <img src="/plus.svg" alt="Plus" />
    </div>
  </div>
</template>
