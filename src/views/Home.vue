<template>
  <div class="home">
    <Navbar />
    <div class="container">
      <Hero />
      <div class="row mt-5 mb-2">
        <div class="col">
          <h2>Best <strong>Foods</strong></h2>
        </div>
        <div class="col">
          <router-link to="/foods" class="btn btn-success float-right"><b-icon-eye class="mr-2" />See more</router-link>
        </div>
      </div>

      <div class="row mb-3">
        <div class="col-md-4 col-6 mb-3" v-for="product in products" v-bind:key="product.id">
          <CardProduct v-bind:product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
// @ is an alias to /src
import Navbar from '@/components/Navbar.vue'
import Hero from '@/components/Hero.vue'
import CardProduct from '@/components/CardProduct.vue'

export default {
  name: 'Home',
  components: {
    Navbar,
    Hero,
    CardProduct
  },
  data () {
    return {
      products: []
    }
  },
  methods: {
    /* ==================== SET PRODUCTS DATA ==================== */
    setProducts: function (data) {
      this.products = data
    },
    /* ==================== GET PRODUCTS FROM API ==================== */
    getProducts: async function () {
      await axios({
        method: 'GET',
        url: 'http://localhost:3000/best-products'
      }).then(res => {
        this.setProducts(res.data)
      }).catch(error => {
        console.log('Failed', error)
      })
    }
  },
  mounted () {
    this.getProducts()
  }
}
</script>
