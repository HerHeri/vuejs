<template>
<div>
  <vue-headful
        title="Kulineran App"
        description="Kulineran App for Web"
    />
  <navbar />
  <div class="container">
    <div class="row mt-3">
      <div class="col">
        <h3>Daftar <strong>Makanan</strong></h3>
      </div>
    </div>

    <div class="row mt-3 mb-3">
      <div class="col">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon1"><b-icon-search></b-icon-search></span>
          </div>
          <input v-model="search" type="text" placeholder="Masukkan Nama Makanan" class="form-control"
          @keyup="searchFood">
        </div>
      </div>
    </div>

    <div class="row mb-3">
      <div class="col-md-3 mt-4" v-for="product in products" :key="product.id">
        <AllFood :product="product"/>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import Navbar from '@/components/navbar.vue'
import AllFood from '@/components/AllFood.vue';
import axios from 'axios'

export default {
    name: "Foods",
    components: {
      Navbar,
      AllFood
    },
    data() {
      return {
        products: [],
        search: ''
      }
    },
    methods: {
      setProduct(data) {
        this.products = data
      },
      searchFood(){
        axios 
        .get('http://localhost:3000/products?q='+this.search)
        .then((response) => this.setProduct(response.data))
        .catch((error) => console.log('Error:', error))  
      }
    },
    mounted() {
      axios 
        .get('http://localhost:3000/products')
        .then((response) => this.setProduct(response.data))
        .catch((error) => console.log('Error:', error))

      // axios.post('http://pretest-qa.dcidev.id/api/v1/register', {
      //     phone: "08080",
      //     country: "inputCountry",
      //     password: "inputPass",
      //     latlong: "-",
      //     device_token: "2",
      //     device_type: "2" // sementara web
      // })
      .then(function (response) {
          console.log(response);
      })
      .catch(function (error) {
          console.error(error);
      });
    }
}
</script>

<style>

</style>