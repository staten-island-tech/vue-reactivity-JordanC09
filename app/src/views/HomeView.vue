<template>
  <div class="navbar bg-neutral text-neutral-content">
    <div class="navbar-start"></div>
    <div class="navbar-center">
      <h1 class="text-xl">Welcome to Your Music Shop</h1>
    </div>
    <div class="navbar-end">
      <div class="flex items-center space-x-2 ml-4">
        <span class="text-lg font-semibold">Balance:</span>
        <span class="text-lg font-bold text-green-500">${{ money }}</span>
      </div>

      <div class="avatar space-x-2 ml-4 relative text-center">
        <div class="w-10 h-10 rounded-full bg-yellow-300">
          <h2 class="text-lg text-zinc-700">{{ level }}</h2>
        </div>
      </div>
    </div>
  </div>
  <div class="bg-cover bg-center h-screen" style="background-image: url('/backdrop.jpg')">
    <nav class="fixed bottom-0 right-0 left-0">
      <RouterLink to="/about"><img src="/cart.webp" alt="cart" class="h-24" /></RouterLink>
    </nav>
    <div class="flex flex-wrap grid grid-cols-3 grid-rows-7 gap-4">
      <AlbumCard v-for="album in instock" :key="album.name" :album="album" :instock="instock">
      </AlbumCard>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { money } from '@/money'
import AlbumCard from '../components/AlbumCard.vue'
import { album } from '../Albumlist.js'
import { instock } from '@/stock'
import { level } from '@/level'

export default {
  components: {
    AlbumCard,
  },
  setup() {
    money
    album
    instock
    level
    const exp = ref(0)
    let tonectlevel = ref(1000)

    let intervalId = null

    const myContinuousFunction = () => {
      if (instock.value.length !== 0) {
        let max = instock.value.length
        let randomNumber = Math.floor(Math.random() * max)

        console.log(instock.value[randomNumber])
        money.value = money.value + instock.value[randomNumber].profit
        let index = instock.value.findIndex(
          (album) => album.profit === instock.value[randomNumber].profit,
        )
        let expgain = Math.floor(instock.value[randomNumber].profit / 2)

        instock.value.splice(index, 1)

        exp.value = exp.value + expgain
        console.log(exp.value)
        if (exp.value >= tonectlevel.value) {
          level.value += 1
          alert('You Leveled Up! New Albums unlocked')
          tonectlevel.value = tonectlevel.value * 10
        }
      }
    }

    onMounted(() => {
      let datime = Math.floor(Math.random() * 10000)
      console.log(datime)
      intervalId = setInterval(myContinuousFunction, datime)
    })

    onBeforeUnmount(() => {
      clearInterval(intervalId)
    })

    return {
      money,
      album,
      instock,
      level,
      exp,
      tonectlevel,
    }
  },
}

//localStorage.setItem();
</script>

<style scoped></style>
