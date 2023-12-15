<script setup>
import Header from './components/Header.vue'
import Card from './components/Card.vue'
</script>

<template>
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header></Header>

    <div class="p-10">
      <h2 class="text-3xl font-bold">All Sneakers</h2>
      <div>
        <Card />
        <Card />
        <Card />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
