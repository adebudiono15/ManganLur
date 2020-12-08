<template>
<div class="container">
     <div class="row hero">
      <div class="col-lg-6">
            <h5><strong>Delicious Food Menu,</strong><br>in Your Gadget</h5>
            <router-link to="/foods" class="btn btn-primary btn-sm shadow"><i class='bx bx-fw bx-right-arrow-alt'></i>Pesan</router-link>
      </div>
      <div class="col-lg-6">
          <img src="../assets/img/hero.png" width="100%">
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
.hero{
    margin-top:120px;
}
</style>