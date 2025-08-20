<script setup>
import { computed, onMounted, provide, ref,  } from 'vue';
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

const cart = ref([]);

const toastList = ref([]);

const addTo = (item)=>{
  const tempItem = {
    id: item.id,
    name: item.title,
    count: 1,
    price: item.price,
  }
  const index = cart.value.findIndex(x=>x.id ===item.id);
  console.log(index, cart.value);
  if (index == '-1'){
    cart.value.push(tempItem);
  }else{
    cart.value[index].count++
  }

  toastList.value.push(item.title)
  setTimeout(()=>{
    toastList.value.shift();
  }, 3000)

}
provide('toastList', toastList)

const tempTotal = computed(()=>{
  return cart.value.reduce(((sum, item)=>{
  return sum+ (item.count * item.price)
}),0)
})

const delItem = (item)=>{
  const index = cart.value.findIndex(x=> x.id == item.id
  )
  cart.value.splice(index,1)
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


    <!-- 購物車區 -->
     <CardList :cart="cart" :temp-total="tempTotal"
     @del-item="delItem"
     />
  </div>

  <!-- 通知元件 -->
   <ToastList :toastList="toastList"
    @del-toast="delToast" />

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
