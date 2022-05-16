<template>
    <div class="card shadow card-product">
        <img :src="'images/'+product.gambar" class="card-img-top" alt="">
        <div class="card-body">
            <h5 class="card-title">{{ product.nama }}</h5>
            <p class="card-text">Harga Rp. {{ product.harga }}</p>
            <a href="" class="btn btn-success" to=""><b-icon-plus></b-icon-plus> Order</a>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Card',
    props: ['product']
}
</script>

<style>
</style>