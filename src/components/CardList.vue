<template>
  <div class="col-md-4">
    <h2 class="mb-3">購物車</h2>
      <div v-if="cart.length > 0">
        <ul class="list-group mb-3">
        <li class="list-group-item d-flex justify-content-between align-items-center" v-for="item in cart" :key="item.id">

          <div>
            <small>訂單編號：{{ item.id }}</small>
            <h6 class="my-0">{{ item.name }}</h6>
            數量： {{ item.count  }}


          </div>
          <div>
            <span class="text-muted">${{ item.price * item.count }}</span>
            <button class="btn btn-sm btn-outline-danger ms-2"
            @click="delItemEmit(item)"
            > 移除 </button>
          </div>

        </li>
      </ul>
      <p class="alert alert-primary">總金額：{{ tempTotal }}</p>
      </div>
      <div v-else>
        <p class="alert alert-danger">尚無商品</p>
      </div>
  </div>
</template>
<script setup>
import { defineProps, defineEmits } from 'vue';

defineProps(['cart', 'tempTotal'])

const emit = defineEmits(['delItem' ])
const delItemEmit = (item)=>{
  emit('delItem', item)
}
</script>
