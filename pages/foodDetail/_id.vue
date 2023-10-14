<template>
  <div class="food-detail">
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <nuxt-link to="/" class="text-dark">Home</nuxt-link>
              </li>
              <li class="breadcrumb-item" aria-current="page">
                <nuxt-link to="/Foods" class="text-dark">Foods</nuxt-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Pesananku
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col-md-6">
          <div class="card mb-4 shadow-sm">
            <img
              :src="'../../_nuxt/assets/images/' + product.gambar"
              :alt="product.gambar"
              class="image-detail shadow"
            />
          </div>
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ product.nama }}</strong>
          </h2>
          <hr />
          <h4>
            Harga:
            <strong>{{ product.harga }}</strong>
          </h4>
          <form class="mt-3" @submit.prevent>
            <div class="form-group">
              <label for="total_pesanan">Mau pesan berapa</label>
              <input
                id="total_pesanan"
                v-model="pesanan.total_pesanan"
                type="number"
                class="form-control"
                placeholder="pesan disini"
              />
            </div>
            <div class="form-group">
              <label for="keterangan">Keterangan</label>
              <textarea
                id="keterangan"
                v-model="pesanan.keterangan"
                class="form-control"
                placeholder="apakah anda ingin memberikan pesan tambahan seperti: ingin pedas atau tidak pedas"
              ></textarea>
            </div>

            <button type="submit" class="btn btn-info" @click="pemesanan">
              <b-icon-cart></b-icon-cart> Pesan
            </button>
          </form>
        </div>
      </div>
    </div>
    <notifications group="foo" position="top right" />
  </div>
</template>
<script>
import { BIconCart } from 'bootstrap-vue'

export default {
  components: {
    BIconCart,
  },
  data() {
    return {
      product: {},
      pesanan: {},
      error: '',
    }
  },
  mounted() {
    this.fetchData()
  },

  methods: {
    async fetchData() {
      try {
        const response = await this.$axios.get(
          '/products/' + this.$route.params.id
        )

        this.setProduct(response.data)
      } catch (error) {
        this.error = error.message
      }
    },

    setProduct(data) {
      this.product = data
    },

    async pemesanan() {
      if (this.pesanan.total_pesanan) {
        this.pesanan.product = this.product
        await this.$axios
          .post('/keranjangs', this.pesanan)
          .then(() => {

            this.$notify({
              group: 'foo',
              type: 'success',
              title: 'Sukses',
              text: 'Pesanan sudah masuk Keranjang',
              duration: 3000,
              closeOnClick: true,
            })
          })
          .catch((err) => console.log(err))
      }else {
        this.$notify({
              group: 'foo',
              type: 'error',
              title: 'Gagal',
              text: 'harap isi total jumlah yang mau kamu pesan',
              duration: 3000,
              closeOnClick: true,
            })
      }
    },
  },
}
</script>

<style>
.breadcrumb-item.active {
  font-weight: bold;
  color: #000;
}

.image-detail {
  width: 100%;
  height: 300px;
  object-fit: cover;
  object-position: center;
  border-radius: 15px;
}
</style>