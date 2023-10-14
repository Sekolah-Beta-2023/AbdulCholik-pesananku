<template>
  <div>
    <div class="card shadow" style="width: 18rem">
      <img
        :src="require(`../assets/images/${product.gambar}`)"
        class="card-img-top card-rounded"
        :alt="product.gambar"
        width="200"
        height="200"
      />
      <div class="card-body">
        <h5 class="card-title">{{ product.nama }}</h5>
        <p class="card-text">Harga: Rp. {{ product.harga }}</p>
        <nuxt-link :to="{name: 'foodDetail-id', params: { id: product.id}}" class="btn btn-primary"
          ><b-icon-cart></b-icon-cart> Pesan</nuxt-link
        >
      </div>
    </div>
  </div>
</template>

<script>
import { BIconCart } from 'bootstrap-vue'

export default {
  name: 'CardProduct',
  components: {
    BIconCart,
  },
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style>
img.card-rounded {
  object-fit: cover;
  object-position: center;
}

.card-rounded {
    border-top-left-radius: 15px;
    border-top-right-radius: 15px;
}
</style>