<template>
<div>
  <navbar />
  <div class="container">
    <Hero />
    <div class="row mt-4">
      <div class="col">
        <h2>Best <strong>Food</strong></h2>
      </div>
      <div class="col">
        <router-link to="/food" class="btn btn-success float-right ">Lihat Semua</router-link>
      </div>
    </div>

    <div class="row mb-3">
      <div class="col-md-4 mt-4" v-for="product in products" :key="product.id">
        <CardProduct :product="product"/>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import Navbar from '@/components/navbar.vue';
import Hero from '@/components/Hero.vue';
import CardProduct from '@/components/Card.vue';
import axios from 'axios'

  export default {
    name: 'Home',
    components: {
        Navbar, 
        Hero,
        CardProduct
    },
    data() {
      return {
        products: []
      }
    },
    methods: {
      setProduct(data) {
        this.products = data
      } 
    },
    mounted() {
      axios 
        .get('http://localhost:3000/best-products')
        .then((response) => this.setProduct(response.data))
        .catch((error) => console.log('Error:', error))
    }
  }
</script>
