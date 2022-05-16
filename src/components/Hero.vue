<template>
    <div class="hero">
        <!-- Web View -->
        <div class="d-none d-md-block">
            <div class="row mt-4">
                <div class="col-md-6">
                    <div class="d-flex h-100">
                        <div class="justify-content-center align-self-center">
                            <h2><strong>Delicious Food Menu,</strong><br> in Your Gadget</h2>
                            <p>Ayo segera pilih makanan favorit anda!</p>
                            <router-link to="/food" class="btn btn-large btn-success">Pesan <b-icon-arrow-right></b-icon-arrow-right></router-link>
                        </div>
                    </div>
                </div>
                <div class="col">
                    <img src="/images/ilustrasi.png" alt="" width="100%">
                </div>
            </div>
        </div>

        <!-- Mobile View -->
        <div class="d-sm-block d-md-none">
            <div class="row mt-4">
                <div class="col">
                    <img src="/images/ilustrasi.png" alt="" width="100%">
                </div>
                <div class="col-md-6 mt-4">
                    <div class="d-flex h-100">
                        <div class="justify-content-center align-self-center">
                            <h2><strong>Delicious Food Menu,</strong><br> in Your Gadget</h2>
                            <p>Ayo segera pilih makanan favorit anda!</p>
                            <router-link to="/food" class="btn btn-large btn-success">Pesan <b-icon-arrow-right></b-icon-arrow-right></router-link>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Hero"
}
</script>

<style>

</style>