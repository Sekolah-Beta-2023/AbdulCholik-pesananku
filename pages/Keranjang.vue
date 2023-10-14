<template>
  <div class="keranjang">
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
                Keranjang
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <h2>Pesanan <strong>Saya</strong></h2>
          <div class="table mt-3">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Foto</th>
                  <th scope="col">Pesanan</th>
                  <th scope="col">Keterangan</th>
                  <th scope="col">Jumlah</th>
                  <th scope="col">Harga</th>
                  <th scope="col">Total Harga</th>
                  <th scope="col">Hapus</th>
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
                      :src="
                        require(`../assets/images/${keranjang.product.gambar}`)
                      "
                      :alt="keranjang.product.gambar"
                      class="img-fluid shadow"
                    />
                  </td>
                  <td>
                    <strong>{{ keranjang.product.nama }}</strong>
                  </td>
                  <td>
                    {{ keranjang.keterangan ? keranjang.keterangan : '-' }}
                  </td>
                  <td>{{ keranjang.total_pesanan }}</td>
                  <td align="right">Rp. {{ keranjang.product.harga }}</td>
                  <td align="right">
                    Rp. {{ keranjang.total_pesanan * keranjang.product.harga }}
                  </td>
                  <td align="center" class="text-danger">
                    <b-icon-trash @click="hapusPesanan(keranjang.id)"></b-icon-trash>
                  </td>
                </tr>

                <tr>
                  <td colspan="6" align="right">
                    <strong>Total Harga :</strong>
                  </td>
                  <td colspan="2" align="center">
                    Rp. <strong>{{ totalHarga }}</strong>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { BIconTrash } from 'bootstrap-vue'

export default {
  components: {
    BIconTrash,
  },
  data() {
    return {
      keranjangs: [],
    }
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce(
        (totalItem, data) =>
          totalItem + data.product.harga * data.total_pesanan,
        0
      )
    },
  },
  mounted() {
    this.fetchKeranjang()
  },
  methods: {
    setKeranjang(data) {
      this.keranjangs = data
    },
    async fetchKeranjang() {
      await this.$axios
        .get('/keranjangs')
        .then((response) => this.setKeranjang(response.data))
        .catch((error) => console.log(error))
    },
    hapusPesanan(id) {
       this.$axios.delete('/keranjangs/' + id)
      .then(() => {
        this.$notify({
          group: 'foo',
          type: 'error',
          title: 'Sukses',
          text: 'Pesanan sudah di hapus',
          duration: 3000,
          closeOnClick: true,
        })

        // update data
        this.$axios
          .get('/keranjangs')
          .then((response) => this.setKeranjangs(response.data))
          .catch((error) => console.log(error))
      })
      .catch(error => console.log(error))
    },
  },
}
</script>

<style scoped>
img {
  width: 250px;
  height: 200px;
  object-fit: cover;
  object-position: center;
}
</style>