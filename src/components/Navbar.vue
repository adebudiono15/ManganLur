<template>
  <nav class="navbar navbar-expand-lg  navbar-light">
      <div class="container">
          <a class="navbar-brand" href="#"><b>Mangan Lur</b></a>
                <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="navbarNav">
                    <ul class="navbar-nav ml-auto">
                    <li class="nav-item mr-5">
                        <router-link class="nav-link" to="/">Home</router-link>
                    </li>
                    <li class="nav-item mr-5">
                        <router-link class="nav-link" to="/foods">Foods</router-link>
                    </li>
                    <li class="nav-item mr-5">
                        <router-link class="nav-link" to="/keranjang">Cart
                            <i class='bx bx-shopping-bag'></i>
                        <span class="badge badge-danger ml-2">{{ updateKeranjang ? updateKeranjang.length : jumlah_pesanans.length }}</span>
                        </router-link>
                    </li>
                    </ul>
                </div>
      </div>
</nav>
</template>

<script>
import axios from "axios";
export default {
    name: "Navbar",
    data(){
        return{
            jumlah_pesanans: []
        }
    },
    props :['updateKeranjang'],
    methods: {
        setJumlah(data){
            this.jumlah_pesanans = data
        }
    },
    mounted() {
        axios.get("http://localhost:3000/keranjangs")
      .then((response) => this.setJumlah(response.data))
      .catch(function (error) {
      })
    },
}
</script>

<style>
.navbar {
    background-color : #00B0FF;
}
.nav-link,.navbar-brand{
    color: #ffffff !important;
}
</style>
