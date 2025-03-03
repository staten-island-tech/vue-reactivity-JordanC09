<template>
  <div class="navbar bg-neutral text-neutral-content">
    <div class="navbar-start">
      <div class="dropdown">
        <div tabindex="0" role="button" class="btn btn-ghost btn-circle">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h16M4 18h7"
            />
          </svg>
        </div>
        <ul
          tabindex="0"
          class="menu menu-sm dropdown-content bg-base-100 rounded-box z-[1] mt-3 w-52 p-2 shadow"
        >
          <li>
            <nav>
              <RouterLink to="/">Home</RouterLink>
            </nav>
          </li>
          <li>
            <nav>
              <RouterLink to="/about">Product Shop</RouterLink>
            </nav>
          </li>
        </ul>
      </div>
    </div>
    <div class="navbar-center">
      <h1 class="text-xl">Product Shop</h1>
    </div>
    <div class="navbar-end">
      <div class="flex items-center space-x-2 ml-4">
        <span class="text-lg font-semibold">Balance:</span>
        <span class="text-lg font-bold text-green-500">${{ money }}</span>
      </div>

      <button class="btn btn-ghost btn-circle">
        <div class="indicator">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
            />
          </svg>
          <span class="badge badge-xs badge-primary indicator-item"></span>
        </div>
      </button>
    </div>
  </div>
  <div>
    <div>
      <!-- <h1>{{ yourcart }}</h1> -->
      <div class="flex flex-wrap grid grid-cols-3 grid-rows-5 gap-4">
        <CartCard
          v-for="album in yourcart"
          :key="album.name"
          :album="album"
          @updateQuantity="updateAlbumQuantity"
        >
        </CartCard>
        <!-- make this in a seperate file and this vue is only for removing js -->
        <button @click="checkout">Checkout</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import AlbumCard from '../components/AlbumCard.vue'
import CartCard from '@/components/CartCard.vue'
import { album } from '../Albumlist.js'
import { yourcart } from '@/cart'
import { money } from '@/money'
import { instock } from '@/stock'

function updateAlbumQuantity(updatedAlbum) {
  let index = yourcart.value.findIndex((a) => a.name === updatedAlbum.name)
  if (index !== -1) {
    yourcart.value[index] = updatedAlbum

    if (updatedAlbum.quantity === 0) {
      let index = yourcart.value.findIndex((a) => a.name === updatedAlbum.name)
      yourcart.value.splice(index, 1)
    }
  }
}
function checkout() {
  let totalcost = 0
  yourcart.value.forEach((album) => {
    if (money.value > 0) {
      if (album.quantity > 1) {
        for (let i = 0; i < album.quantity; i++) {
          totalcost = totalcost + album.price
          instock.value.push(album)
        }
      } else {
        totalcost = totalcost + album.price
        instock.value.push(album)
      }
    }
  })

  money.value = money.value - totalcost
  album.forEach((album) => (album.quantity = 0))

  yourcart.value = []
}

//just make album in a vue to make it reactive
</script>

<style scoped></style>
