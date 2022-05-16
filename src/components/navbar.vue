<template>
    <div>
        <b-navbar toggleable="lg" type="light">
            <div class="container">
                <b-navbar-brand href="#"> <strong>Kulineran</strong></b-navbar-brand>

                <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

                <b-collapse id="nav-collapse" is-nav>
                    <b-navbar-nav>
                        <router-link class="nav-link" aria-current="page" to="/">Home</router-link>
                        <router-link class="nav-link" to="/food">Food</router-link>
                    </b-navbar-nav>

                    <!-- Right aligned nav items -->
                    <b-navbar-nav class="ml-auto">
                        <ul class="navbar-nav ml-auto">
                            <li class="nav-item">
                                <router-link class="nav-link" aria-current="page" to="/keranjang">
                                    Keranjang &nbsp;
                                    <b-icon-bag></b-icon-bag>
                                    <span class="badge badge-success" v-on:update.prevent>{{ updateKeranjang ? updateKeranjang.length : jumlah_pesanan.length }}</span>
                                </router-link>
                            </li>
                        </ul>
                    </b-navbar-nav>
                </b-collapse>
            </div>
        </b-navbar>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: "navbar",
    data() {
        return {
            jumlah_pesanan: []
        }
    },
    props: ['updateKeranjang'],
    methods: {
        setJumlah(data) {
            this.jumlah_pesanan = data
        }
    }, 
    mounted(){
        axios 
        .get('http://localhost:3000/keranjangs')
        .then((response) => this.setJumlah(response.data))
        .catch((error) => console.log('Error:', error))
    }
}
</script>

<style>

</style>