<script setup>
import NestedList from './NestedList.vue';
import data from '../data'
import { onClickOutside } from '@vueuse/core'
import { ref,onMounted,onUnmounted } from 'vue'
const show = ref(false)

const toggleHandler = () => {
  show.value = !show.value
}

const showParentId = ref(null)
const setCurrentParentId = (id) => {
  if(showParentId.value === id) {
    showParentId.value = null
  }else {
    showParentId.value = id
  }
}

let stopClickListener
const menuRef = ref(null)

onMounted(() => {
  stopClickListener = onClickOutside(menuRef, () => {
    if (show.value) {
      show.value = false
    }
  })
})
onUnmounted(() => stopClickListener && stopClickListener())

</script>

<template>
  <button class="text-2xl" @click="toggleHandler">
    ≡
  </button>
  <section class="bg-gray-700 h-full w-1/2 absolute bottom-0 left-0" v-show="show" ref="menuRef">
    <ul class="p-4">
      <li v-for="item in data.data" :key="item.key" class="mb-3" @click.stop="setCurrentParentId(item.key)" :class="{'text-yellow-600' : item.key === showParentId}">
        {{ item.text }}
        <NestedList :items="item.children" :show="item.key === showParentId" />
      </li>
    </ul>
    
  </section>
</template>
