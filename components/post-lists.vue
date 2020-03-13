<template>
    <tbody>
        <tr>
            <td>{{id}}</td>
            <td>{{useriId}}</td>
            <td>{{title}}</td>
            <td>{{body}}</td>
            <td>
                <nuxt-link :to="'/tampil/' + id">
                    <button class="btn btn-sm btn-primary">Detail</button>
                </nuxt-link>
                <nuxt-link :to="'/tampil/' + id + '/edit'">
                    <button class="btn btn-sm btn-primary">Edit</button>
                </nuxt-link>
                <nuxt-link :to="'/tampil/' + id">
                    <button @click="hapus" class="btn btn-sm btn-primary">Delete</button>
                </nuxt-link>
            </td>
        </tr>
    </tbody>
</template>

<script>
import Axios from 'axios'
export default {
    props:{
        id: {
            type: String,
            default: ''
        },
        useriId: {
            type: String,
            default: ''
        },
        title:{
            type: String,
            default: ''
        },
        body:{
            type: String,
            default: ''
        },
    },
    methods:{
        hapus(){
            const hapus1 = confirm('Apakah anda yakin ingin mengahapus data?')
            if(!hapus1){
                return
            };
            const hapus2 = confirm('Apakah anda benar - benar yakin ingin menghapus data ini?')
            if(!hapus2){
                return
            };
            Axios.delete('http://localhost:3001/posts/' + this.id)
            .then((del) => {
                this.$emit('muat-ulang');
            });
        },
    }
}
</script>