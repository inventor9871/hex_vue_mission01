<script setup>
import { computed, onMounted, ref,  } from 'vue';
import ProductList from '@/components/ProductList.vue';
import CardList from '@/components/CardList.vue';
import ToastList from '@/components/ToastList.vue';


const products = ref();
onMounted(()=>{
  products.value = [
    {
      id:1,
      imgUrl: 'https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&amp;w=2065&amp;auto=format&amp;fit=crop&amp;ixlib=rb-4.1.0&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
      title: '耳罩式藍牙耳機',
      description: '舒適配戴，支援降噪技術',
      price: 1111
    },
    {
      id:2,
      imgUrl: 'https://images.unsplash.com/photo-1613040809024-b4ef7ba99bc3?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
      title: '粉紅耳機',
      description: '可以展現力與美',
      price: 2222
    },
    {
      id:3,
      imgUrl: 'https://images.unsplash.com/photo-1635329086694-d02f81549dea?q=80&w=435&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
      title: '迷你耳機',
      description: '無憂無慮',
      price: 3333
    },
  ]
})

const temp = ref([]);

const toastList = ref([]);

const addTo = (item)=>{
  //  console.log('item : ',item)
  const now = new Date();
  const year = now.getFullYear();
  const month = now.getMonth() + 1; // getMonth() 回傳 0-11，所以要 +1
  const day = now.getDate();
  const hours = now.getHours();
  const minutes = now.getMinutes();
  const seconds = now.getSeconds();
  const milliseconds = now.getMilliseconds();

  const time = `${year}${month}${day}${hours}${minutes}${seconds}${milliseconds}`;

  const tempItem = {
    id: time,
    name: item.title,
    count: 1,
    price: item.price,
  }

  temp.value.push(tempItem);

  toastList.value.push(item.title)
  setTimeout(()=>{
    toastList.value.shift();
  }, 3000)

}



const tempTotal = computed(()=>{
  return temp.value.reduce(((sum, item)=>{
  return sum+ (item.count * item.price)
}),0)
})

const delItem = (item)=>{
  const index = temp.value.findIndex(x=> x.id == item.id
  )
  // console.log(index)
  temp.value.splice(index,1)
}

const delToast = (index)=>{
  toastList.value.splice(index,1);
}

</script>

<template>
  <div id="app" class="container py-4">
  <div class="row">
    <!-- 商品列表區 -->
     <ProductList :products="products"
      @addTo="addTo"
     />
     <!-- @click="addTo" -->
    <!-- <div cl`ass="col-md-8">`
      <h2 class="mb-3">商品列表</h2>
      <div class="row">
        <div class="col-md-4 mb-4" v-for="item in products" :key="item.id">
          <div class="card h-100">
            <img :src="item.imgUrl" class="card-img-top">
            <div class="card-body">
              <h5 class="card-title">{{ item.title }}</h5>
              <p class="card-text">{{ item.description }}</p>
              <p class="fw-bold text-primary">$ {{ item.price }}</p>
              <button class="btn btn-success w-100" @click="addTo(item)"> 加入購物車 </button>
            </div>
          </div>
        </div>
      </div>
    </div> -->

    <!-- 購物車區 -->
     <CardList :temp="temp" :temp-total="tempTotal"
     @del-item="delItem"
     />
    <!-- <div class="col-md-4">
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
            @click="delItem(item)"
            > 移除 </button>
          </div>

        </li>
      </ul>
      <a v-if="temp.length > 0"  class="btn btn-outline-primary">總金額：{{ tempTotal }}</a>
    </div> -->
  </div>

  <!-- 通知元件 -->
   <ToastList :toastList="toastList"
    @del-toast="delToast" />
  <!-- <div class="position-fixed top-0 end-0 p-3" style="z-index: 1050" v-if="toastList.length>0">
    <div class="toast show align-items-center text-white bg-success border-0" v-for="(item, index) in toastList" :key="item.id"
    style="margin: 2px;" >
      <div class="d-flex">
        <div class="toast-body">
         您已訂購 {{ item }}</div>

        <button type="button" class="btn-close btn-close-white me-2 m-auto" @click="delToast(index)"></button>
      </div>
    </div>
  </div> -->

</div>
</template>
<style>
@import url(https://cdnjs.cloudflare.com/ajax/libs/bootstrap/5.0.2/css/bootstrap.min.css);
body {
  background: #f2f2f2f2;
}

.card-img-top {
  height: 150px;
  object-fit: cover;
}

</style>
