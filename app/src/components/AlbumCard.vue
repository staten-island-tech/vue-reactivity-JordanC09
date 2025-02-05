<template>
  <div
    class="rounded-box bg-red-500 flex-1 max-w-100 flex-auto justify-around items-center p-6 m-4"
  >
    <h2 class="text-lg">{{ album.name }}</h2>
    <img class="w-full h-full pb-6" :src="album.image" alt="" />
  </div>
</template>

<script setup>
defineProps({
  album: Object,
  //pass in the animal which is an object
})
</script>

<style scoped></style>
