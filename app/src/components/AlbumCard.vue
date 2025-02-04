<template>
  <div class="flex">
    <div class="flex-auto flex-wrap shrink justify-between justify-around items-center">
      <h2>{{ album.name }}</h2>
      <img :src="album.image" alt="" />
    </div>
  </div>
</template>

<script setup>
defineProps({
  album: Object,
  //pass in the animal which is an object
})
</script>

<style scoped></style>
