<template>
  <div>
    <nuxt-link :to="'/li-kategori'">
      <button class="btn btn-md btn-primary">Back</button>
    </nuxt-link>
    <nuxt-link :to="'/li-kategori/' + id + '/edit'">
      <button class="btn btn-md btn-warning">Edit</button>
    </nuxt-link>
    <nuxt-link :to="'#'">
      <button class="btn btn-md btn-danger">Delete</button>
    </nuxt-link>
    <h1>{{kategori.title}}</h1>
    <p>{{kategori.body}}</p>
    <p>User Id ={{kategori.userId}}</p>
  </div>
</template>

<script>
import Axios from "axios";
export default {
  data() {
    return {
      kategori: {},
      id: this.$route.params.kategoriId
    };
  },
  mounted() {
    Axios.get(
      "http://localhost:3001/kategoris/" + this.$route.params.kategoriId
    ).then(res => {
      this.kategori = res.data || {};
    });
  }
};
</script>