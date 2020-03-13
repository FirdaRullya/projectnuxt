<template>
  <div>
    <nuxt-link :to="'/li-kategori'">
      <button class="btn btn-md btn-primary">Back</button>
    </nuxt-link>

    <h1>Form Edit Data</h1>
    <form>
      <input type="text" name="userId" v-model="kategori.userId" placeholder="Kategori Kue" />
      <input type="text" name="title" v-model="kategori.title" placeholder="Nama Kue" />
      <input type="text" name="body" v-model="kategori.body" placeholder="Keterangan" />
      <button class="btn btn-md btn-success" @click.prevent="simpan">Submit</button>
    </form>
  </div>
</template>

<script>
import Axios from "axios";
export default {
  data() {
    return {
      kategori: {}
    };
  },
  mounted() {
    this.getDetail();
  },
  methods: {
    getDetail() {
      Axios.get(
        "http://localhost:3001/kategoris/" + this.$route.params.kategoriId
      ).then(res => {
        this.kategori = res.data || {};
      });
    },
    simpan() {
      Axios.patch(
        "http://localhost:3001/kategoris/" + this.$route.params.kategoriId,
        this.kategori
      ).then(send => {
        this.$router.push("/li-kategori");
      });
    }
  }
};
</script>