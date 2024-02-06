<script setup>
import { ref } from 'vue'
import Axios from 'axios'
const products = ref(null)
Axios.get("http://localhost:3000/products").then( r=>{
  products.value = r.data
} )

function postToCart(productId){
  let foundItem;
  Axios.get("http://localhost:3000/cart/" + productId).then(r => {if(r.status == 200) foundItem = r.data})
  let cartAmount = 1;
  if(foundItem) cartAmount = ++foundItem.amount;
  const cartItem = {
    id: productId,
    amount: cartAmount
  }
  Axios.post("http://localhost:3000/cart",cartAmount).then( r => {
    alert("Hozzáadva a kosárhoz!")
  })
}
</script>

<template>
<div class="container">
  <div class="row align-items-center">
    <div class="card col-lg-3 col-md-6 col-12" v-for="product in products">
          <img src="../assets/no-image.png" alt="no image"/>
          <div>{{ product.name }}</div>
          <div>{{  product.price }}</div>
          <button @click="postToCart(product.id)" class="btn-primary btn">Kosárba!</button>
        </div>
  </div>
</div>
</template>

<style scoped>
.card {
  padding: 1rem;
  margin: 1rem;
}
</style>
