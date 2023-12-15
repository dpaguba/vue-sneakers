<script setup>
import Header from './components/Header.vue'
</script>

<template>
  <div class="bg-white w-4/5 h-screen m-auto rounded-xl shadow-xl mt-14">
    <Header></Header>

    <div>
      <div
        class="relative m-10 border border-slate-100 rounded-3xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition"
      >
        <img src="/like-2.svg" alt="Like 1" class="absolute top-8 left-8" />
        <img src="/sneakers/sneakers-1.jpg" alt="Sneaker" />
        <p class="mt-2">Nike Blazer Mid Suede</p>

        <div class="flex justify-between mt-5">
          <div class="flex flex-col">
            <span class="text-slate-400">Price:</span>
            <b> 120$ </b>
          </div>
          <img src="/plus.svg" alt="Plus" />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
