<template>
    <div class="keranjang">
        <Navbar :updateKeranjang="keranjangs" />
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
                        <router-link to="">Keranjang</router-link>
                    </li>
                    </ol>
                </nav>
                </div>
            </div>


            <div class="row mt-3" v-on:submit.prevent>
                <div class="col">
                    <h2>Keranjang <strong>Saya</strong></h2>
                    <div class="table-responsive mt-5">
                        <table class="table">
                            <thead>
                                <tr>
                                    <th scope="col">#</th>
                                    <th scope="col">Foto</th>
                                    <th scope="col">Nama Makanan</th>
                                    <th scope="col">Keterangan</th>
                                    <th scope="col">Jumlah</th>
                                    <th scope="col">Harga</th>
                                    <th scope="col">Total Harga</th>
                                    <th scope="col">Hapus</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(keranjang, index) in keranjangs" :key="keranjang.id">
                                    <th scope="row">{{ index+1 }}</th>
                                    <td><img :src="'../images/'+keranjang.products.gambar" class="img-fluid shadow" alt="" width="250px"></td>
                                    <td>{{ keranjang.products.nama }}</td>
                                    <td>{{ keranjang.keterangan ? keranjang.keterangan : "-" }}</td>
                                    <td>{{ keranjang.jumlah_pemesanan }}</td>
                                    <td align="center">Rp. {{ keranjang.products.harga }}</td>
                                    <td style="font-weight:bold" align="center">Rp. {{ keranjang.products.harga * keranjang.jumlah_pemesanan }}</td>
                                    <td align="center"><b-icon-trash v-on:submit.prevent @click="hapusKeranjang(keranjang.id)" style="color:red"></b-icon-trash></td>
                                </tr>

                                <tr>
                                    <td colspan="6" align="right">
                                        <strong>Total Harga: </strong> 
                                    </td>
                                    <td align="right">
                                        <strong>Rp. {{ totalHarga }}</strong>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- Form Checkout -->
            <div class="row justify-content-end">
                <div class="col-md-4">
                    <form v-on:submit.prevent class="mt-4">
                        <div class="form-group">
                            <label for="">Nama</label>
                            <input type="text" class="form-control" v-model="pesan.nama">
                        </div>
                        <div class="form-group">
                            <label for="">Nomor Meja</label>
                            <input type="text" class="form-control" v-model="pesan.noMeja">
                        </div>
                        
                        <button type="submit" class="btn btn-success" style="color: white" @click="checkout">
                            <b-icon-cart></b-icon-cart>&nbsp; Order
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import Navbar from '@/components/navbar.vue'
import axios from 'axios'

export default {
    name: "Keranjang",
    components: {
      Navbar,
    },
    data() {
        return {
            keranjangs: [],
            pesan: {}
        }
    },
    methods: {
        setKeranjang(data){
            this.keranjangs = data
        },
        hapusKeranjang(id){
            axios 
            .delete('http://localhost:3000/keranjangs/'+id)
            .then(() =>{
                this.$toasted.show('Sukses Menghapus Menu di Keranjang', {
                    type: 'error',
                    position: 'top-right',
                    dismissible: true
                })

                // Update data keranjang
                axios 
                .get('http://localhost:3000/keranjangs/')
                .then((response) => this.setKeranjang(response.data))
                .catch((error) => console.log('Error:', error))
            })
            .catch((error) => console.log('Error:', error))
        },
        checkout() {
            if(this.pesan.nama && this.pesan.noMeja){
                this.pesan.keranjangs = this.keranjangs;
                axios 
                    .post('http://localhost:3000/pesanans/', this.pesan)
                    .then(() => {

                        // Hapus Semua Keranjang    
                        this.keranjangs.map(function (item) {
                            return axios
                                .delete('http://localhost:3000/keranjangs/'+item.id)
                                .catch((error) => console.log('Error:', error))
                        })

                        this.$router.push({ path: "/pesanansukses" }),
                        this.$toasted.show('Pemesanan berhasil, silahkan ditunggu', {
                            type: 'success',
                            position: 'top-right',
                            dismissible: true
                        })
                    })
                    .catch((error) => console.log('Error:', error))
            }else{
                this.$toasted.show('Nama dan Nomor Meja Wajib diisi', {
                    type: 'error',
                    position: 'top-right',
                    dismissible: true
                })
            }
        }
    },
    mounted(){
        axios 
        .get('http://localhost:3000/keranjangs/')
        .then((response) => this.setKeranjang(response.data))
        .catch((error) => console.log('Error:', error))
    },
    computed:{
        totalHarga(){
            return this.keranjangs.reduce(function(items,data){
                return items+(data.products.harga*data.jumlah_pemesanan)
            },0)
        }
    }
}
</script>

<style>

</style>