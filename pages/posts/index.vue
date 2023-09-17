<script setup lang="ts">

    //meta title
    useHead({
        title: 'Data notes - isam samsul arip',
    });

    //init config
    const config = useRuntimeConfig();

    //fetch data from API with "useAsyncData"
    const { data: notes } : any = await useAsyncData('notes', () => $fetch(`${config.public.apiBase}/api/notes`))

    //method deletePost
    const deletePost = async (id: number) => {

        //delete data with API
        await $fetch(`${config.public.apiBase}/api/notes/${id}`, {

            //method
            method: 'DELETE'
        });

        //refersh data posts
        refreshNuxtData('notes');
    }

</script>

<template>
    <div class="container mt-5 mb-5">
        <div class="row">
            <div class="col-md-12">
                <NuxtLink to="/posts/create" class="btn btn-md btn-success rounded shadow border-0 mb-3">ADD NEW NOTES</NuxtLink>
                <div class="card border-0 rounded shadow">
                    <div class="card-body">
                        <table class="table table-bordered">
                            <thead class="bg-dark text-white">
                                <tr>
                                    <th scope="col">Title</th>
                                    <th scope="col">Content</th>
                                    <th scope="col" style="width:15%">Actions</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(post, index) in notes" :key="index">
                                    <td>{{ post.title }}</td>
                                    <td>{{ post.content }}</td>
                                    <td class="text-center">
                                        <NuxtLink :to="`/posts/edit/${post.id}`" class="btn btn-sm btn-primary rounded-sm shadow border-0 me-2">EDIT</NuxtLink>
                                        <button @click="deletePost(post.id)" class="btn btn-sm btn-danger rounded-sm shadow border-0">DELETE</button>
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