<template>
    <div>
        <h1>Daftar Kue</h1>
        <nuxt-link :to="'/li-post/create'">
            <button class="btn btn-md btn-info">Tambah Daftar Kue</button>
        </nuxt-link>
        <input type="text" v-model="cari" placeholder="Cari Kue Apa ?">
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
            <PostList
            v-for="post in filteredPosts"
            :key="post.id"
            :id="post.id"
            :userId="post.userId"
            :title="post.title"
            :body="post.body"
            @muat-ulang="getData"
            ></PostList>
        </table>
        <b-button v-else variant="primary" disabled>
            <b-spinner small type="grow"></b-spinner>
                Loading...
        </b-button>
    </div>
</template>

<script>
import Axios from 'axios';
import PostList from '~/components/post-lists';
export default {
    components:{
        PostList,
    },
    data(){
        return{
            posts:[],
            isError: false,
            isLoading: false,
            isEmpty:false,
            cari:'',
        }
    },
    mounted(){
        this.getData()
    },
    methods: {
        async getData(){
            this.isLoading = true;
            try{
                const res = await Axios.get('http://localhost:3001/posts');
                this.posts = res.data;
                if(this.posts.length === 0){
                    this.isEmpty = true;
                };
            }catch(err){
                console.log('error!');
                console.error(err);
                this.isError = true;
            }this.isLoading = false;
        }
    },
    computed:{
        filteredPosts: function(){
            return this.posts.filter((post) => {
                return post.title.match(this.cari);
            });
            return this.posts.filter((post) => {
                return post.kategoriId.match(this.cari);
            });
        },
    }
}
</script>