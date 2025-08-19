<template>
  <div class="col-md-4">
      <h2 class="mb-3">購物車</h2>
      <ul class="list-group mb-3">
        <li class="list-group-item d-flex justify-content-between align-items-center" v-for="item in temp" :key="item.id">

          <div>
            <small>訂單編號：{{ item.id }}</small>
            <h6 class="my-0">{{ item.name }}</h6>
            數量：
            <input class="text-muted" type="number" v-model="item.count" min="0" max="10"/>

          </div>
          <div>
            <span class="text-muted">${{ item.price * item.count }}</span>
            <button class="btn btn-sm btn-outline-danger ms-2"
            @click="delItemEmit(item)"
            > 移除 </button>
          </div>

        </li>
      </ul>
      <p v-if="temp.length > 0"  class="alert alert-primary">總金額：{{ tempTotal }}</p>
    </div>
</template>
<script setup>
import { defineProps, defineEmits } from 'vue';
defineProps(['temp', 'tempTotal'])
const emit = defineEmits(['delItem' ])
const delItemEmit = (item)=>{
  emit('delItem', item)
}
</script>
