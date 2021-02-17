<template>
  <div class="cart">
    <Navbar :updateKeranjang="keranjangs" />
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
                My Cart
              </li>
            </ol>
          </nav>
        </div>
      </div>
      <!-- End of Breadcrumb Section -->

      <!-- Cart Content Section -->
      <div class="row">
        <div class="col">
          <h2>My <strong>Cart</strong></h2>
          <div class="table-responsive mt-3">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Picture</th>
                  <th scope="col">Food</th>
                  <th scope="col">Note</th>
                  <th scope="col">Quantity</th>
                  <th scope="col">Price</th>
                  <th scope="col">Total</th>
                  <th scope="col">Delete</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="(keranjang, index) in keranjangs"
                  :key="keranjang.id"
                >
                  <th>{{ index + 1 }}</th>
                  <td>
                    <img
                      :src="'../assets/images/' + keranjang.products.gambar"
                      :alt="keranjang.products.nama"
                      class="img-fluid shadow"
                      width="200"
                    />
                  </td>
                  <td>
                    <strong>{{ keranjang.products.nama }}</strong>
                  </td>
                  <td>
                    {{ keranjang.keterangan ? keranjang.keterangan : "-" }}
                  </td>
                  <td align="center">{{ keranjang.jumlah_pemesanan }}</td>
                  <td align="right">Rp {{ keranjang.products.harga }}</td>
                  <td align="right">
                    <strong
                      >Rp
                      {{
                        keranjang.products.harga * keranjang.jumlah_pemesanan
                      }}</strong
                    >
                  </td>
                  <td align="center" class="text-danger">
                    <b-icon-trash
                      style="cursor: pointer"
                      @click="deleteKeranjangs(keranjang.id)"
                    />
                  </td>
                </tr>
                <tr>
                  <td colspan="6" align="right">
                    <strong>Total Harga : </strong>
                  </td>
                  <td align="right">
                    <strong>Rp {{ totalHarga }}</strong>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
      <!-- End of Cart Content Section -->

      <!-- Checkout Form -->
      <div class="row justify-content-end">
        <div class="col-md-4">
          <form class="mt-4" v-on:submit.prevent="">
            <div class="form-group">
              <label for="nama">Nama</label>
              <input
                type="text"
                class="form-control"
                v-model="pesan.nama"
              />
            </div>
            <div class="form-group">
              <label for="noMeja">Nomor Meja</label>
              <input
                type="text"
                class="form-control"
                v-model="pesan.noMeja"
              />
            </div>

            <button type="submit" class="btn btn-success float-right" @click="checkout">
              <b-icon-cart class="mr-2" />Order
            </button>
          </form>
        </div>
      </div>
      <!-- End of Checkout Form -->
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Navbar from '@/components/Navbar.vue'

export default {
  name: 'Cart',
  components: {
    Navbar
  },
  data () {
    return {
      keranjangs: [],
      pesan: {}
    }
  },
  methods: {
    setKeranjang: function (data) {
      this.keranjangs = data
    },
    getKeranjang: async function () {
      await axios({
        method: 'GET',
        url: 'http://localhost:3000/keranjangs'
      })
        .then((res) => this.setKeranjang(res.data))
        .catch((error) => console.log(error))
    },
    deleteKeranjangs: async function (id) {
      await axios({
        method: 'DELETE',
        url: `http://localhost:3000/keranjangs/${id}`
      })
        .then(() => {
          this.$toast.success('Delete Success', {
            type: 'success',
            position: 'top-right',
            duration: 3000,
            dismissible: true
          })
          this.getKeranjang()
        })
        .catch((error) => console.log(error))
    }
  },
  created () {
    this.getKeranjang()
  },
  computed: {
    totalHarga: function () {
      return this.keranjangs.reduce((items, data) => {
        return items + data.products.harga * data.jumlah_pemesanan
      }, 0)
    }
  }
}
</script>

<style>
</style>
