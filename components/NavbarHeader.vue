<template>
  <div>
    <b-navbar toggleable="lg" type="light">
      <div class="container">
        <b-navbar-brand href="#">Pesananku</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <li class="nav-item">
              <nuxt-link
                class="nav-link d-none d-md-block"
                exact-active-class="font-weight-bold"
                to="/"
                >Home</nuxt-link
              >
            </li>
            <li class="nav-item d-none d-md-block">
              <nuxt-link
                class="nav-link"
                exact-active-class="font-weight-bold"
                to="/Foods"
                >Foods</nuxt-link
              >
            </li>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <li class="nav-item">
              <nuxt-link
                class="nav-link font-weight-bold"
                exact-active-class="font-weight-bold"
                to="/registrasi"
                >Registrasi</nuxt-link
              >
            </li>
            <li class="nav-item">
              <nuxt-link class="nav-link font-weight-bold" to="/login"
                >Login</nuxt-link
              >
            </li>
            <li class="nav-item">
              <nuxt-link
                class="nav-link d-none d-md-block"
                to="/Keranjang"
                exact-active-class="font-weight-bold"
              >
                Keranjang
                <b-icon-bag></b-icon-bag>
                <span class="badge badge-info ml-2">{{total_pesanan.length}}</span>
              </nuxt-link>
            </li>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
import { BIconBag } from 'bootstrap-vue'
export default {
  components: {
    BIconBag,
  },
  data() {
    return {
      total_pesanan: []
    }
  },
  async fetch() {
    await this.$axios
       .get('/keranjangs')
       .then(response => this.setOrder(response.data))
       .catch(error => console.log(error))
  },
  methods: {
    setOrder(data) {
      this.total_pesanan = data
    },

  }
}
</script>

<style>
</style>