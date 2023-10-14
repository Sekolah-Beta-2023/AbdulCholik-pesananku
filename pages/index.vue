<template>
  <div class="home">
    <div class="container">
      <HeroMenu />

      <div class="row mt-4">
        <div class="col">
          <h2>Makanan <strong>Terlaris</strong></h2>
        </div>
        <div class="col">
          <nuxt-link to="/Foods" class="btn btn-info float-right"
            ><b-icon-eye></b-icon-eye> Semua</nuxt-link
          >
        </div>
      </div>

      <div class="row mb-4">
        <div
          v-for="product in products"
          :key="product.id"
          class="col-md-4 mt-4"
        >
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { BIconEye } from 'bootstrap-vue'
import HeroMenu from '@/components/HeroMenu.vue'
import CardProduct from '@/components/CardProduct.vue'

export default {
  name: 'IndexPage',
  components: {
    HeroMenu,
    BIconEye,
    CardProduct,
  },
  data() {
    return {
      products: [],
      error: '',
    }
  },
  mounted() {
    this.fetchData()
  },
  methods: {
    async fetchData() {
      try {
        const response = await this.$axios.get('/best-products')
        // console.log(response)
        this.products = response.data
      } catch (error) {
        this.error = error.message
      }
    },
  },
}
</script>
