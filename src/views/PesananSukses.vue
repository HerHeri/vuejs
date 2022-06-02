<template>
    <div class="pesanansukses">
        <vue-headful
            title="Kulineran App"
            description="Kulineran App for Web"
        />
        <Navbar />
        <div class="container">
            <div class="row justify-content-center mt-5">
                <div class="col text-center">
                    <img src="/images/menunggu.png" alt="" width="20%"><br>
                    <h2><strong>Berhasil</strong></h2>
                    <span style="font-size: 20px">Makanan berhasil dipesan, <br> silahkan ditunggu</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Navbar from '@/components/navbar.vue'
export default {
    nama: "PesananSukses",
    components: {
        Navbar
    }
}
</script>

<style>

</style>