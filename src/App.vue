<script setup>
import Sidebar from './components/Sidebar.vue'
</script>

<template>
  <div class="py-2 px-4 bg-gray-800 text-white h-screen">
    <Sidebar  />
    <div class="text-2xl">
      <div class="grid">
        <div class="item relative" v-for="item in 9" :key="item" :class="{'animate-pulse': (item === 3 || item === 5 || item === 9)}">
          <div class="ball absolute bottom-10 left-0" v-show="item <= 3 || item >=7" 
          :class="{
            'delay1': item === 2 || item === 8,
            'delay2': item === 3 || item === 9,
          }"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 30px;
  margin-top: 10px;
}

.item {
  height: 100px;
  border: 2px solid black;
  background: radial-gradient(circle, rgba(113,81,95,1) 81%, rgba(0,0,0,1) 100%);
}

.ball {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background-color: #A5F12B;
  transform: translate(-50%, -50%);
  animation: move .8s linear infinite;
}

@keyframes move {
  0% {
    left: 0;
  }
  100% {
    left: 100%;
  }
}
.delay1 {
  animation-delay: 1s;
}
.delay2 {
  animation-delay: 2s;
}
</style>