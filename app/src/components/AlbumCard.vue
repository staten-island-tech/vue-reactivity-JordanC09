<template>
  <div
    class="text-neutral-content text-center rounded-box bg-gray-500 flex-1 max-w-100 flex-auto justify-around items-center p-6 m-4"
  >
    <h2 class="uppercase text-clamp">{{ album.name }}</h2>
    <img class="w-full h-90 pb-6" :src="album.image" alt="" />

    <slot></slot>
    <!-- https://daisyui.com/components/card/ -->
  </div>
</template>

<script>
export default {
  name: 'AlbumCard',
  props: {
    album: Object,
  },
  // Other component logic here
};
</script>

<style scoped></style>
