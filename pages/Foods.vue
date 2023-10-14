<template>
  <div class="container">
    <div class="row mt-4">
      <div class="col">
        <h2><strong>Menu</strong></h2>
      </div>
    </div>

    <div class="row mt-3">
      <div class="col">
        <div class="input-group mb-3">
          <input
            v-model="search"
            type="text"
            class="form-control"
            placeholder="Mau makan apa hari ini ?"
            aria-label="Cari Makanan"
            aria-describedby="basic-addon1"
            @keyup="searchFoods"
          />

          <div class="input-group-prepend">
            <span id="basic-addon1" class="input-group-text">
              <b-icon-search></b-icon-search>
            </span>
          </div>
        </div>
      </div>
    </div>

    <div class="row mb-4">
      <div v-for="product in products" :key="product.id" class="col-md-4 mt-4">
        <CardProduct :product="product" />
      </div>
    </div>
  </div>
</template>

<script>
import { BIconSearch } from 'bootstrap-vue'
import CardProduct from '@/components/CardProduct.vue'

export default {
  name: 'Foods',
  components: {
    CardProduct,
    BIconSearch,
  },
  data() {
    return {
      products: [],
      error: '',
      search: '',
    }
  },
  mounted() {
    this.fetchData()
  },
  
  methods: {
    async fetchData() {
      try {
        const response = await this.$axios.get('/products')

        this.setProducts(response.data)
      } catch (error) {
        this.error = error.message
      }
    },
    
    setProducts(data) {
      this.products = data
    },
    async searchFoods() {
      try {
        const response = await this.$axios.get('/products?q=' + this.search)

        this.setProducts(response.data)
      }
      catch (error) {
        this.error = error.message
      }
    },
  },
}
</script>
  
<style>
</style>