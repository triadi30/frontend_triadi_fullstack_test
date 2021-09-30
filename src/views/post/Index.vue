<template>
    <div class="container mt-5">
        <div class="row">
            <div class="col-md-12">
                <div class="card border-0 rounded shadow">
                    <div class="card-body">
                        <h4>DATA ASET</h4>
                        <hr>
                        <router-link :to="{name: 'post.create'}" class="btn btn-md btn-success">TAMBAH ASET
                        </router-link>

                        <table class="table table-striped table-bordered mt-4">
                            <thead class="thead-dark">
                                <tr>
                                    <th scope="col">Nomor</th>
                                    <th scope="col">Kode Unik</th>
                                    <th scope="col">QR Code</th>
                                    <th scope="col">OPTIONS</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(post, index) in posts" :key="index">
                                    <td>{{ index+1 }}</td>
                                    <td>{{ post.kode_unik }}</td>
                                    <td>
                                        <img src="{{ post.link_qr_code }}" alt="" title="" />
                                    </td>
                                    <td class="text-center">
                                        <router-link :to="{name: 'post.edit', params:{id: post.id }}"
                                            class="btn btn-sm btn-primary mr-1">EDIT</router-link>
                                        <button class="btn btn-sm btn-danger ml-1">DELETE</button>
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
    import axios from 'axios'
    import {
        onMounted,
        ref
    } from 'vue'

    export default {

        setup() {

            //reactive state
            let posts = ref([])

            //mounted
            onMounted(() => {

                //get API from Laravel Backend
                axios
                    .get('http://localhost:8000/v1/aset/')
                    .then(response => {

                        //assign state posts with response data
                        posts.value = response.data.data

                    }).catch(error => {
                        console.log(error.response)
                        //console.log(posts.value)
                    })

            })

            //return
            return {
                posts
            }
        }

    }
</script>

<style>
    body {
        background: lightgray;
    }
</style>