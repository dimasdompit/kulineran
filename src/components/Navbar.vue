<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <div class="container">
        <b-navbar-brand href="#">Kulineran</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <li class="nav-item">
              <router-link class="nav-link" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/foods">Foods</router-link>
            </li>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <router-link class="nav-link" to="/cart">
              Cart
              <span class="badge badge-success ml-2">{{
                updateKeranjang
                  ? updateKeranjang.length
                  : jumlah_pesanans.length
              }}</span>
              <b-icon-bag></b-icon-bag>
            </router-link>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Navbar',
  props: ['updateKeranjang'],
  data () {
    return {
      jumlah_pesanans: []
    }
  },
  methods: {
    setJumlah: function (data) {
      this.jumlah_pesanans = data
    }
  },
  async created () {
    await axios({
      method: 'GET',
      url: 'http://localhost:3000/keranjangs'
    })
      .then((res) => {
        this.setJumlah(res.data)
      })
      .catch((error) => {
        console.log('Failed', error)
      })
  }
}
</script>

<style>
</style>
