<template>
  <div class="col-md-8">
      <h2 class="mb-3">商品列表</h2>
      <div class="row">
        <div class="col-md-4 mb-4" v-for="item in products" :key="item.id">
          <div class="card h-100">
            <img :src="item.imgUrl" class="card-img-top">
            <div class="card-body">
              <h5 class="card-title">{{ item.title }}</h5>
              <p class="card-text">{{ item.description }}</p>
              <p class="fw-bold text-primary">$ {{ item.price }}</p>
              <button class="btn btn-success w-100" @click="addToEmit(item)"> 加入購物車 </button>

            </div>
          </div>
        </div>
      </div>
    </div>
</template>
<script setup>

defineProps(['products'])

const emit = defineEmits(['addTo'])
const addToEmit = (item)=>{
  emit('addTo', item)
}
</script>
