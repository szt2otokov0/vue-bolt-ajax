<script setup>
import { ref } from 'vue'
import Axios from 'axios'
const products = ref(null)
Axios.get("http://localhost:3000/products").then( r=>{
  products.value = r.data
} )

function postToCart(product){
  Axios.post("http://localhost:3000/cart",product).then( r => {
    alert("Hozzáadva a kosárhoz!")
  })
}
</script>

<template>
<div class="container">
  <div class="row align-items-center">
    <div class="card col-lg-2 col-md-4 col-12" v-for="product in products">
          <img src="../assets/no-image.png" alt="no image"/>
          <div>{{ product.name }}</div>
          <div>{{  product.price }}</div>
          <button @click="postToCart(product)" class="btn-primary btn">Kosárba!</button>
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
