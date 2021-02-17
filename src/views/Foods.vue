<template>
  <div class="foods">
    <!-- Navbar Component -->
    <Navbar />
    <div class="container">
    <!-- Heading -->
      <div class="row mt-4">
        <div class="col">
          <h2>Foods <strong>Menu</strong></h2>
        </div>
      </div>

      <!-- Input Search -->
      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3 search-input-group">
            <input
              type="text"
              class="form-control search-input"
              placeholder="Search Your Favorite Foods"
              aria-label="Search"
              aria-describedby="basic-addon1"
              v-model="search"
              v-on:keyup="searchProducts"
            />
            <div class="input-group-prepend">
              <span class="input-group-text" id="basic-addon1"><b-icon-search /></span>
            </div>
          </div>
        </div>
      </div>

      <!-- Card All Foods -->
      <div class="row mb-3">
        <div
          class="col-md-4 col-6 mb-3"
          v-for="product in products"
          v-bind:key="product.id"
        >
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
import CardProduct from '@/components/CardProduct.vue'

export default {
  name: 'Foods',
  components: {
    Navbar,
    CardProduct
  },
  data () {
    return {
      products: [],
      search: ''
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
        url: 'http://localhost:3000/products'
      })
        .then((res) => {
          this.products = res.data
        })
        .catch((error) => {
          console.log(error)
        })
    },
    /* ==================== SEARCH PRODUCTS FROM API ==================== */
    searchProducts: async function () {
      await axios({
        method: 'GET',
        url: `http://localhost:3000/products/?q=${this.search}`
      })
        .then((res) => {
          this.products = res.data
        })
        .catch((error) => {
          console.log(error)
        })
    }
  },
  mounted () {
    this.getProducts()
  }
}
</script>

<style>
</style>
