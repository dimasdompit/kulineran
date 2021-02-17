<template>
  <div class="food-details">
    <Navbar />
    <div class="container">
      <!-- Breadcrumb Section -->
      <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-dark">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Food Order
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <!-- End of Breadcrumb Section -->

      <!-- Food Description Section -->
      <div class="row mt-3">
        <div class="col-md-6">
          <img
            :src="'../assets/images/' + product.gambar"
            :alt="product.nama"
            class="img-fluid shadow mb-3"
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <h4>
            Price : <strong>Rp {{ product.harga }}</strong>
          </h4>
          <form class="mt-4" v-on:submit.prevent="">
            <div class="form-group">
              <label for="jumlah_pemesanan">Order Quantity</label>
              <input
                type="number"
                class="form-control"
                v-model="pesan.jumlah_pemesanan"
              />
            </div>
            <div class="form-group">
              <label for="keterangan">Note</label>
              <textarea
                class="form-control"
                placeholder="Ex: Pedas, Nasi Setengah, etc"
                v-model="pesan.keterangan"
              ></textarea>
            </div>

            <button type="submit" class="btn btn-success" @click="pemesanan">
              <b-icon-cart class="mr-2" />Order
            </button>
          </form>
        </div>
      </div>
      <!-- End of Food Description Section -->
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Navbar from '@/components/Navbar.vue'

export default {
  name: 'FoodDetails',
  components: {
    Navbar
  },
  data () {
    return {
      product: {},
      pesan: {}
    }
  },
  methods: {
    setProductDetails: function (data) {
      this.product = data
    },
    pemesanan: async function () {
      if (this.pesan.jumlah_pemesanan && this.pesan.jumlah_pemesanan >= 1) {
        this.pesan.products = this.product
        await axios({
          method: 'POST',
          url: 'http://localhost:3000/keranjangs',
          data: this.pesan
        })
          .then((res) => {
            this.$router.push({ path: '/cart' })
            this.$toast.success('Add to Cart Success', {
              type: 'success',
              position: 'top-right',
              duration: 3000,
              dismissible: true
            })
          })
          .catch((error) => {
            console.log(error)
          })
      } else {
        this.$toast.error('Order Quantity Minimum 1', {
          type: 'error',
          position: 'top-right',
          duration: 3000,
          dismissible: true
        })
      }
    }
  },
  async created () {
    await axios({
      method: 'GET',
      url: `http://localhost:3000/products/${this.$route.params.id}`
    })
      .then((res) => {
        this.setProductDetails(res.data)
      })
      .catch((error) => {
        console.log(error)
      })
  }
}
</script>

<style>
</style>
