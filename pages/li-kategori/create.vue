<template>
  <div>
    <nuxt-link :to="'/li-kategori'">
      <button class="btn btn-md btn-primary">Back</button>
    </nuxt-link>

    <h1>Form Daftar Kue</h1>
    <form>
      <input type="number" name="userId" v-model="kategori.userId" placeholder="Kategori Kue" />
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
  methods: {
    simpan() {
      Axios.kategori("http://localhost:3001/kategoris", this.kategori).then(
        send => {
          this.$router.push("/li-kategori");
        }
      );
    }
  }
};
</script>