<template>
  <div class="mt-5">
    <nav
      id="bottom-nav"
      class="navbar navbar-dark bg-info navbar-expand d-md-none d-lg-none d-xl-none p-0 m-"
    >
      <ul class="navbar-nav nav-justified w-100">
        <li class="nav-item">
          <nuxt-link
            to="/"
            class="nav-link"
            exact-active-class="font-weight-bold"
          >
            <b-icon-house-fill></b-icon-house-fill>
            <h6>Home</h6>
          </nuxt-link>
        </li>
        <li class="nav-item">
          <nuxt-link
            to="/Foods"
            class="nav-link"
            exact-active-class="font-weight-bold"
          >
            <b-icon-card-list></b-icon-card-list>
            <h6>Foods</h6>
          </nuxt-link>
        </li>
        <li class="nav-item">
          <nuxt-link
            to="/Keranjang"
            class="nav-link"
            exact-active-class="font-weight-bold"
          >
            <b-icon-bag></b-icon-bag
            ><span class="badge badge-warning ml-2">{{total_pesanan.length}}</span>
            <h6>Keranjang</h6>
          </nuxt-link>
        </li>
        <li class="nav-item">
          <nuxt-link
            to="/profile"
            class="nav-link"
            exact-active-class="font-weight-bold"
          >
            <b-icon-person-fill></b-icon-person-fill>
            <h6>Profil</h6>
          </nuxt-link>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
import {
  BIconHouseFill,
  BIconCardList,
  BIconBag,
  BIconPersonFill,
} from 'bootstrap-vue'

export default {
  name: 'BottomNavbar',
  components: {
    BIconHouseFill,
    BIconCardList,
    BIconBag,
    BIconPersonFill,
  },
  data() {
    return {
      total_pesanan: []
    }
  },
  mounted() {
    this.totalOrder()
  },
  methods: {
    setOrder(data) {
      this.total_pesanan = data
    },
    async totalOrder() {
      try {
        await this.$axios.get('/keranjangs')
        .then(response => this.setOrder(response.data))
      }
      catch(error) {
        console.log(error)
      }
    }
  }
}
</script>

<style>
#bottom-nav {
  width: 100%;
  position: fixed;
  bottom: 0;
  z-index: 2;
}
</style>