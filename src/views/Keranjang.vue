<template>
  <div class="keranjang">
    <Navbar :updateKeranjang="keranjangs"/>
      <div class="container">
          <div class="row mt-5">
              <h5><strong>Keranjang </strong> saya</h5>
          </div>
          <div class="row">
              <div class="table-responsive mt-5">
                    <table class="table">
                            <thead>
                                <tr>
                                <th scope="col">#</th>
                                <th scope="col">Foto</th>
                                <th scope="col">Makanan</th>
                                <th scope="col">Keterangan</th>
                                <th scope="col">Jumlah</th>
                                <th scope="col">Harga</th>
                                <th scope="col">Total Harga</th>
                                <th scope="col">Hapus</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(keranjang,index) in keranjangs" :key="keranjang.id">
                                <th>{{ index+1 }}</th>
                                <td><img :src="'../img/' +keranjang.products.gambar" alt="Card image cap" width="250"></td>
                                <td>{{ keranjang.products.nama }}</td>
                                <td class="text-center">
                                    {{ keranjang.keterangan ? keranjang.keterangan : "-" }}
                                </td>
                                <td>{{ keranjang.jumlah_pemesanan }}</td>
                                <td align="right">Rp. {{ keranjang.products.harga }}</td>
                                <td align="right"><strong>Rp. {{ keranjang.products.harga*keranjang.jumlah_pemesanan }}</strong></td>
                                <td align="center">
                                    <button class="btn btn-sm btn-primary mt-0 mb-0"  @click="hapusKeranjang(keranjang.id)">
                                        <i class='bx bxs-trash bx-fw bx-lg' style='color:#fff'  ></i>
                                    </button>
                                </td>
                                </tr>
                                <tr>
                                    <td colspan="8" align="right">
                                        <strong>Total Harga : {{ totalHarga }}</strong>
                                    </td>
                                </tr>
                            </tbody>
                    </table>
              </div>
          </div>

          <div class="row justify-content-end mt-5">
                    <div class="col-md-4">
                        <form v-on:submit.prevent>
                                    <div class="form-group">
                                        <label for="nama">
                                                <small class="form-text text-muted">Nama Pemesan</small>
                                        </label>
                                        <input type="text" class="form-control" aria-describedby="helpId" v-model="pesan.nama">
                                    </div>
                                    <div class="form-group">
                                        <label for="noMeja">
                                                <small class="form-text text-muted">Nomor Meja</small>
                                        </label>
                                        <input type="number" class="form-control" aria-describedby="helpId" v-model="pesan.noMeja">
                                    </div>
                                    <button type="submit" class="btn btn-sm btn-primary mt-0 mb-0" @click="checkout">Pesan</button>
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
    name : "Keranjang",
    data(){
        return{
            keranjangs : [],
            pesan: {}
        }
    },
    methods: {
        setKeranjangs(data){
            this.keranjangs = data;
        },

        checkout(){
            if(this.pesan.nama && this.pesan.noMeja){
                this.pesan.keranjangs = this.keranjangs;
                axios.post("http://localhost:3000/pesanans/", this.pesan)
                .then(() => {
                this.keranjangs.map(function(item){
                    axios.delete("http://localhost:3000/keranjangs/"+ item.id)
                });
                this.$router.push({ path: "/" })
               this.$toast.success("Sukses Memesan", {
                type: "success",
                position : "top-right",
                duration : 3000,
                dismissible :true,
                });
                 // update data keranjang
             axios.get("http://localhost:3000/keranjangs")
            .then((response) => this.setKeranjangs(response.data))
            .catch(function (error) {
            })
            })
            }else{
                 this.$toast.error("Isi Nama Dan No Meja Untuk Memesanan", {
                type: "error",
                position : "top-right",
                duration : 3000,
                dismissible :true,
                });
            }
        },
        hapusKeranjang(id){
             axios.delete("http://localhost:3000/keranjangs/"+id)
            .then(() => {
                this.$router.push({ path: "/keranjang" })
               this.$toast.success("Sukses Hapus Makanan", {
                type: "success",
                position : "top-right",
                duration : 3000,
                dismissible :true,
                });
                 // update data keranjang
             axios.get("http://localhost:3000/keranjangs")
            .then((response) => this.setKeranjangs(response.data))
            .catch(function (error) {
            })
            })
        }
    },
    mounted(){
    axios.get("http://localhost:3000/keranjangs/")
      .then((response) => this.setKeranjangs(response.data))
      .catch(function (error) {});
    },
    computed: {
        totalHarga() {
            return this.keranjangs.reduce(function(items, data){
                return items+(data.products.harga*data.jumlah_pemesanan)
            }, 0)
            }
        }
    }
   
</script>