<script setup>
import NestedList from './NestedList.vue'
import { defineProps, ref } from 'vue'

defineProps({
  items: {
    type: Array,
    default: () => []
  },
  show: {
    type: Boolean,
    default: false
  }
})

const showChildId = ref(null)
const setCurrentChildId = (id) => {
  if(showChildId.value === id) {
    showChildId.value = null
  }else {
    showChildId.value = id
  }
}

</script>

<template>
  <ul class="pl-2 pt-2 text-white" v-show="show && items.length">
    <li class="mb-3" @click.stop="setCurrentChildId(item.key)" v-for="item in items" :key="item.key" :class="{'text-yellow-600' : item.key === showChildId}">
      {{ item.text }}
      <NestedList :items="item?.children" :show="item.key === showChildId" class="pl-2"/>
    </li>
  </ul>
</template>
