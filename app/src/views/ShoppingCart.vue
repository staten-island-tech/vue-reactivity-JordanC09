<template>
  <div>
    <h2>this my shopping cart dog</h2>
    <nav>
      <RouterLink to="/about">Product shop</RouterLink>
    </nav>
    <div>
      <h1>{{ yourcart }}</h1>
      <div class="flex flex-wrap grid grid-cols-3 grid-rows-5 gap-4">
        <AlbumCard v-for="album in yourcart" :key="album.name" :album="album" :yourcart="yourcart">
          <h3>Quantity: {{ album.quantity }}</h3>
          <button @click="removeitem(album)">Remove Item</button>
        </AlbumCard>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import AlbumCard from '../components/AlbumCard.vue'
import { album } from '../Albumlist.js'
import { yourcart } from '../cart.js'

function removeitem(removedalbum) {
  if (removedalbum.quantity > 1) {
    removedalbum.quantity--
  }
}
</script>

<style scoped></style>
