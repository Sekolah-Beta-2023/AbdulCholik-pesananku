<template>
  <div class="row">
    <div class="col">
      <div class="d-flex h-100">
        <div class="justify-content-center align-self-center">
          <h2>
            <strong>Pesan Menu Apapun</strong>, makanan/minuman semaumu
            <br />hanya dari gadgetmu
          </h2>
          <p>Pilih makanan dan minuman yang kamu mau hanya disini</p>
          <nuxt-link to="/Foods" class="btn btn-lg btn-info">
            <b-icon-arrow-right></b-icon-arrow-right> Pesan
          </nuxt-link>
        </div>
      </div>
    </div>
    <div class="col">
      <img class="d-md-flex d-none" src="@/assets/hero.png" alt="hero image" width="100%" />
    </div>
  </div>
</template>

<script>
import { BIconArrowRight } from 'bootstrap-vue'

export default {
  name: 'HeroMenu',
  components: {
    BIconArrowRight,
  },
}
</script>

<style>
.nuxt-link-exact-active {
  font-weight: bold;
}
</style>