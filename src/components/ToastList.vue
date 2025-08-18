<template>
  <div class="position-fixed top-0 end-0 p-3" style="z-index: 1050" v-if="toastList.length>0" >
    <div class="toast show align-items-center text-white bg-success border-0" v-for="(item, index) in toastList" :key="index"
    style="margin: 2px;" >
      <div class="d-flex">
        <div class="toast-body">
         您已訂購 {{ item }}</div>

        <button type="button" class="btn-close btn-close-white me-2 m-auto" @click="delToastEmit(index)"></button>
      </div>
    </div>
  </div>
</template>
<script setup>
import { defineProps, defineEmits } from 'vue';
defineProps(['toastList'])
const emit = defineEmits(['delToast'])
const delToastEmit = (index)=>{
  emit('delToast', index)
}
</script>
