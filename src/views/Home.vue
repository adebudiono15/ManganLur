<template>
  <div class="home">
     <Navbar :updateKeranjang="keranjangs"/>
    <Hero/>
    <div class="container">
      <div class="row mt-5">
        <div class="col-lg-6">
          <h5 class="mt-5"><strong>Best</strong> Menu</h5>
        </div>
      </div>

      <div class="row mt-5 justify-content-center text-center">
        <div class="col-lg-4" v-for="product in products" :key="product.id">
          <CardProduct :product="product"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'
import Hero from '@/components/Hero.vue'
import CardProduct from '@/components/CardProduct.vue'
import Navbar from '@/components/Navbar.vue'

export default {
  name: 'Home',
  components: {
    Hero,
    CardProduct,
    Navbar
  },
  
  data(){
    return{
      keranjangs : [],
      products: []
    }
  },
  methods: {
    setProduct(data){
      this.products = data;
    }
  },
  mounted(){
    axios.get("http://localhost:3000/best-products")
      .then((response) => this.setProduct(response.data))
      .catch(function (error) {
      })
  },
};
</script>