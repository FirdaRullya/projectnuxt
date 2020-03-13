<template>
    <div>
        <nuxt-link :to="'/li-post'">
            <button class="btn btn-md btn-primary">Back</button>
        </nuxt-link>

        <h1>Form Edit Data</h1>
        <form>
            <input type="number" name="userId" v-model="post.userId" placeholder="Kategori Kue">
            <input type="text" name="title" v-model="post.title" placeholder="Nama Kue">
            <input type="text" name="body" v-model="post.body" placeholder="Keterangan">
            <button class="btn btn-md btn-success" @click.prevent="simpan">Submit</button>
        </form>
    </div>
</template>

<script>
import Axios from 'axios'
export default {
    data(){
        return{
            post:{},
        };
    },
    mounted(){
        this.getDetail()
    },
    methods:{
        getDetail(){
            Axios.get('http://localhost:3001/posts/' + this.$route.params.postId)
            .then((res) =>{
                this.post = res.data || {}
            })
        },
        simpan(){
            Axios.patch('http://localhost:3001/posts/' + this.$route.params.postId,
            this.post
            )
            .then((send) =>{
                this.$router.push('/li-post')
            })
        },
    },
}
</script>