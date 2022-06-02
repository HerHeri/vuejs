<template>
  <div>
    <vue-headful
        title="Kulineran App"
        description="Kulineran App for Web"
    />
    <div class="food-detail">
      <Navbar/>
      <div class="container">
  
        <!-- Breadcrumb -->
        <div class="row mt-3">
          <div class="col">
            <nav aria-label="breadcrumb">
              <ol class="breadcrumb">
                <li class="breadcrumb-item">
                  <router-link to="/" class="text-dark">Home</router-link>
                </li>
                <li class="breadcrumb-item">
                  <router-link to="/food" class="text-dark">Food</router-link>
                </li>
                <li class="breadcrumb-item active">
                  <router-link to="">Food Detail</router-link>
                </li>
              </ol>
            </nav>
          </div>
        </div>
  
        <!-- Food Detail -->
        <div class="row">
          <div class="col-md-6">
            <img :src="'../images/'+product.gambar" class="img-fluid shadow" alt="">
          </div>
          <div class="col-md-6">
            <h2>{{ product.nama }}</h2>
            <hr>
            <h4>Harga : Rp. {{ product.harga }}</h4>
            <form v-on:submit.prevent class="mt-4">
              <div class="form-group">
                <label for="">Jumlah Pesan</label>
                <input type="number" class="form-control" v-model="pesan.jumlah_pemesanan">
              </div>
              <div class="form-group">
                <label for="keterangan">Keterangan</label>
                <textarea placeholder="Pedas, Nasi Setengah" id="" class="form-control" v-model="pesan.keterangan"></textarea>
              </div>
              <button type="submit" class="btn btn-success" style="color: white" @click="pemesanan"><b-icon-cart></b-icon-cart>Order</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from '@/components/navbar.vue'
import axios from 'axios'
export default {
  name: "FoodDetail",
  components: {
    Navbar
  },
  data(){
    return {
      product: {},
      pesan: {}
    }
  },
  methods:{
    setProduct(data){
      this.product = data
    },
    pemesanan(){
      // console.log(this.product);
      if (this.pesan.jumlah_pemesanan) {
        this.pesan.products = this.product
        
        axios 
          .post('http://localhost:3000/keranjangs', this.pesan)
          this.$router.push({ path: "/keranjang"})
          .then(() => {
            this.$toasted.show('Sukses masuk keranjang', {
              type: 'success',
              position: 'top-right',
              dismissible: true
            })
          })
          .catch((error) => console.log('Error:', error))
      } else {
        this.$toasted.show('Silahkan isi jumlah pesanan anda', {
          type: 'error',
          position: 'top-right',
          dismissible: true
        })
      }
    }
  },
  mounted() {
      axios 
        .get('http://localhost:3000/products/'+this.$route.params.id)
        .then((response) => this.setProduct(response.data))
        .catch((error) => console.log('Error:', error))
    }
}
</script>

<style>

</style>