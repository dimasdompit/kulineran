<template>
  <div class="card shadow card-product">
    <img :src="'../assets/images/' + product.gambar" class="card-img-top" />
    <div class="card-body">
      <h5 class="card-title">{{ product.nama }}</h5>
      <p class="card-text card-price">Rp {{ product.harga }}</p>
      <router-link v-bind:to="'/foods/' + product.id" class="btn btn-success"
        ><b-icon-cart class="mr-2" />Pesan</router-link
      >
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardProduct',
  props: ['product']
}
</script>
