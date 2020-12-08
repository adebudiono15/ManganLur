<template>
<div class="Detail-foods">
    <Navbar/>
    <div class="container">
            <div class="row mt-5">
                <h5>Detail <strong>Foods</strong></h5>
            </div>

            <div class="row  mt-5 mb-5">
                <div class="col-lg-6">
                    <img class="card-img-top" :src="'../img/' +product.gambar" alt="Card image cap">
                </div>
                <div class="col-lg-6">
                    <h4><b>{{ product.nama }}</b></h4>
                    <h6>Rp. {{ product.harga }}</h6>
                    <hr>
                    <form v-on:submit.prevent>
                    <div class="form-group">
                        <label for="jumlah_pemesanan">
                                <small class="form-text text-muted">Order Quantity</small>
                        </label>
                      <input type="number" class="form-control" aria-describedby="helpId" v-model="pesan.jumlah_pemesanan">
                    </div>

                    <div class="form-group">
                        <label for="keterangan">
                                <small class="form-text text-muted">Order Quantity</small>
                        </label>
                     <small class="form-text text-muted">Information</small>
                      <textarea class="form-control"  rows="3" placeholder="Hot...." v-model="pesan.keterangan"></textarea>
                    </div>
                    <button type="submit" class="btn btn-sm btn-primary shadow" @click="pemesanan">Pesan</button>
                    </form>
                </div>
            </div>
    </div>
</div>

</template>

<script>
import axios from 'axios'
import Navbar from '@/components/Navbar.vue'


export default {
    components:{
    Navbar
    },
    name : 'FoodDetail',
    data(){
        return{
            product : {},
            pesan: {}
        };
    },
    methods:{
        setProduct(data){
            this.product = data;
        },
        pemesanan(){
            if(this.pesan.jumlah_pemesanan){
            this.pesan.products = this.product;
            axios.post("http://localhost:3000/keranjangs", this.pesan)
            .then(() => {
                this.$router.push({ path: "/keranjang" })
               this.$toast.success("Sukses Masuk Keranjang", {
                type: "success",
                position : "top-right",
                duration : 3000,
                dismissible :true,
                });
            })
            } else{
                this.$toast.error("Gagal Masuk Keranjang", {
                type: "error",
                position : "top-right",
                duration : 3000,
                dismissible :true,
                });
            }
            // console.log (this.pesan)
        }
    },
     mounted(){
    axios.get("http://localhost:3000/products/"+this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch(function (error) {});
  }
};
</script>