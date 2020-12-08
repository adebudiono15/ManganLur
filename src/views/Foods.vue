<template>
<div class="Foods">
      <Navbar/>
       <div class="container">
      <div class="row justify-content-center mt-5 mb-5">
        <h5>Daftar <strong>Mangan</strong></h5>
      </div>
        <div class="row justify-content-center">
          <div class="col-lg-6">
            <label class="sr-only" for="inlineFormInputGroupUsername2">Search Foods</label>
              <div class="input-group mb-2 mr-sm-2">
                <input type="text" class="form-control" id="inlineFormInputGroupUsername2" placeholder="Search Foods" v-model="search" @keyup="searchFoods">
                <div class="input-group-prepend">
                  <div class="input-group-text"><i class='bx bx-search-alt'></i></div>
                </div>
              </div>
          </div>
        </div>
        <div class="row mt-5 justify-content-center text-center">
            <div class="col-lg-4 mt-4 mb-4" v-for="product in products" :key="product.id">
              <CardProduct :product="product"/>
            </div>
        </div>
    </div>
</div>
   
</template>
<script>
// @ is an alias to /src
import axios from 'axios'
import Navbar from '@/components/Navbar.vue'
import CardProduct from '@/components/CardProduct.vue'

export default {
  name: 'Foods',
  components: {
    CardProduct,
    Navbar
  },
  data(){
    return{
      products: [],
      search : '',
    }
  },
  methods: {
    setProduct(data){
      this.products = data;
    },
    searchFoods(){
       axios.get("http://localhost:3000/products?q="+this.search)
      .then((response) => this.setProduct(response.data))
      .catch(function (error) {
      })
    }
  },
  mounted(){
    axios.get("http://localhost:3000/products")
      .then((response) => this.setProduct(response.data))
      .catch(function (error) {
      })
  },
}
</script>