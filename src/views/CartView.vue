<script setup>
import { ref } from 'vue'
import Axios from 'axios'
const products = ref(null)

Axios.get("http://localhost:3000/cart").then(r => products.value = r.data)
</script>

<template>
    <h1>A kosár</h1>
    <ul>
        <li v-for="product in products" class="card">
            {{ product.name }}
        </li>
    </ul>
</template>

<style scoped></style>