<template>
  <div class="bg-[url(/public/space.jpeg)]"></div>
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
      <div class="flex-none">
        <div class="dropdown dropdown-end">
          <div tabindex="0" role="button" class="btn btn-ghost btn-circle">
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
                  d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"
                />
              </svg>
              <span class="badge badge-sm indicator-item">8</span>
            </div>
          </div>
          <div
            tabindex="0"
            class="card card-compact dropdown-content bg-base-100 z-[1] mt-3 w-52 shadow"
          >
            <div class="card-body">
              <span class="text-lg font-bold">8 Items</span>
              <span class="text-info">Subtotal: $999</span>
              <div class="card-actions rounded-box bg-gray-500 justify-around items-center">
                <nav>
                  <RouterLink to="/cart">Go To Cart</RouterLink>
                </nav>
              </div>
            </div>
          </div>
        </div>
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
  <main>
    <div class="flex flex-wrap grid grid-cols-3 grid-rows-5 gap-4">
      <AlbumCard v-for="album in album" :key="album.name" :album="album">
        <button @click="addtocart(album.name)" class="btn btn-neutral">${{ album.price }}</button>
      </AlbumCard>
    </div>
  </main>
</template>

<script setup>
import { ref, reactive } from 'vue'
import AlbumCard from '../components/AlbumCard.vue'
import { album } from '../Albumlist.js'
import { yourcart } from '../cart.js'

//bruh figure it out
function addtocart(name) {
  yourcart.push(name)

  console.log(yourcart)
}
</script>

<style scoped></style>
