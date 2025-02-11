<template>
  <div>
    <h2>this my shopping cart dog</h2>
    <nav>
      <RouterLink to="/about">Product shop</RouterLink>
    </nav>
    <div>
      <h1>{{ yourcart }}</h1>
      <div class="flex flex-wrap grid grid-cols-3 grid-rows-5 gap-4">
        <AlbumCard v-for="album in yourcart" :key="album.name" :album="album">
          <button @click="addtocart(album.name)" class="btn btn-neutral">${{ album.price }}</button>
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
</script>

<style scoped></style>
