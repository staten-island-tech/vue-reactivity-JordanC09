<template>
<div class="navbar bg-neutral text-neutral-content">
  <div class="navbar-start">
    
  </div>
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
        <h2 class="text-lg text-zinc-700">5</h2>
      </div> 
    </div>
  </div>
</div>
<div class="bg-cover bg-center h-screen" style="background-image: url('/backdrop.jpg');">
  
    
  <nav class="fixed bottom-0 right-0 left-0">
    <RouterLink to="/about"><img src="/cart.webp" alt="cart" class="h-24"></RouterLink>
  </nav>
  
  
  
  
  
</div>

  
</template>


<script>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import {money} from '@/money'
import AlbumCard from '../components/AlbumCard.vue'
import { album } from '../Albumlist.js'
import {instock} from '@/stock'



export default {
  setup() {
    money; 
    
    let intervalId = null; 

    
    const myContinuousFunction = () => {
      money.value++;
      
    };

    
    onMounted(() => {
      intervalId = setInterval(myContinuousFunction, 1000); 
    });

    
    onBeforeUnmount(() => {
      clearInterval(intervalId);
    });

    return {
      money, 
    };
  },
};

//localStorage.setItem();
</script>


<style scoped></style>
