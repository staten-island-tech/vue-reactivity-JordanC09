<template>
    <div
      class="text-neutral-content text-center rounded-box bg-gray-500 flex-1 max-w-100 flex-auto justify-around items-center p-6 m-4"
    >
      <h2 class="uppercase text-clamp">{{ album.name }}</h2>
      <img class="w-full h-90 pb-6" :src="album.image" alt="" />
      <h3>Quantity: {{ album.quantity }}</h3>
      <button @click="removeitem(album)">Remove Item</button>
  
      <slot></slot>
      <!-- https://daisyui.com/components/card/ -->
    </div>
</template>
  
<script setup>
defineProps({
    album: Object,
    //pass in the animal which is an object
})
import { yourcart } from '@/cart'
    
let emit = defineEmits(['updateQuantity'])

function removeitem(album) {
    
    console.log(album.quantity)
    let updatedAlbum = { ...album };
    
    
    updatedAlbum.quantity--  
    console.log(album.quantity)

    
    emit('updateQuantity', updatedAlbum);
    
    console.log(yourcart)
    
    console.log(album)
    
}        
    
</script>
  
<style scoped></style>