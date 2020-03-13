<template>
  <div>
    <h1>Kategori</h1>
    <nuxt-link :to="'/li-kategori/create'">
      <button class="btn btn-md btn-info">Tambah Daftar Kue</button>
    </nuxt-link>
    <input type="text" v-model="cari" placeholder="Cari Kue Apa ?" />
    <!-- ISI CONTENT -->
    <h1 v-if="isError">Ini Error</h1>
    <h1 v-else-if="isEmpty">Data Kosong</h1>
    <table v-else-if="!isLoading" border="1 solid">
      <thead>
        <tr>
          <th>ID</th>
          <th>Kategori ID</th>
          <th>Nama Kue</th>
          <th>Keterangan</th>
          <th>Action</th>
        </tr>
      </thead>
      <KategoriList
        v-for="kategori in filteredKategoris"
        :key="kategori.id"
        :id="kategori.id"
        :userId="kategori.userId"
        :title="kategori.title"
        :body="kategori.body"
        @muat-ulang="getData"
      ></KategoriList>
    </table>
    <b-button v-else variant="primary" disabled>
      <b-spinner small type="grow"></b-spinner>Loading...
    </b-button>
  </div>
</template>

<script>
import Axios from "axios";
import KategoriList from "~/components/kategori-lists";
export default {
  components: {
    KategoriList
  },
  data() {
    return {
      kategoris: [],
      isError: false,
      isLoading: false,
      isEmpty: false,
      cari: ""
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    async getData() {
      this.isLoading = true;
      try {
        const res = await Axios.get("http://localhost:3001/kategoris");
        this.kategoris = res.data;
        if (this.kategoris.length === 0) {
          this.isEmpty = true;
        }
      } catch (err) {
        console.log("error!");
        console.error(err);
        this.isError = true;
      }
      this.isLoading = false;
    }
  },
  computed: {
    filteredKategoris: function() {
      return this.kategoris.filter(kategori => {
        return kategoris.title.match(this.cari);
      });
      return this.kategoris.filter(kategori => {
        return kategoris.userId.match(this.cari);
      });
    }
  }
};
</script>