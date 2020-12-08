<template>
  <div>
         <div class="card shadow">
            <img class="card-img-top" :src="'../img/' +product.gambar" alt="Card image cap">
            <div class="card-body">
                <p class="card-title">{{ product.nama }}</p>
                <p class="card-text">Harga : Rp.{{ product.harga }}</p>
                <router-link :to="'/foods/'+product.id" class="btn tbn-sm btn-primary pesan">Pesan</router-link>
            </div>
        </div>
  </div>
</template>

<script>
export default {
    name: "CardProduct",
    props: ['product']
}
</script>

<style>
.pesan{
    margin-top : 0px !important;
}
</style>