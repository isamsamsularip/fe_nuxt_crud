<script setup lang="ts">
 import { Response } from 'node-fetch'; // Add this import
    //meta title
    useHead({
        title: 'Edit a Notes - Isam Samsul Arip',
    });

    //init config
    const config = useRuntimeConfig();  

    //init router
    const router = useRouter();

    //init route
    const route = useRoute();

    //fetch daa for get detail data post
    const { data: post } : any = await useFetch(`${config.public.apiBase}/api/notes/${route.params.id}`);
    

    //define state
    const title     = ref(post.value.title);
    const content   = ref(post.value.content);
    const errors  : any  = ref({});

   // method "updatePost"
   const updatePost = async () => {
        if (!title.value || !content.value) {
            errors.value = {
                title: ['Title is required'],
                content: ['Content is required'],
            };
            return; // Stop further execution if validation fails
        }

        try {
            const response = await $fetch(`${config.public.apiBase}/api/notes/${route.params.id}`, {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json', // Set content type to JSON
                },
                body: JSON.stringify({
                    title: title.value,
                    content: content.value,
                    _method: 'PATCH',
                }),
            });
            router.push({ path: "/posts" });
        } catch (error) {
            // Handle network or other errors
            console.error('Error:', error);
        }
    }
</script>

<template>
    <div class="container mt-5">
        <div class="row">
            <div class="col-md-12">
                <div class="card border-0 rounded shadow">
                    <div class="card-body">
                        <form @submit.prevent="updatePost()">
                            <div class="mb-3">
                                <label class="form-label fw-bold">Title</label>
                                <input type="text" class="form-control" v-model="title" placeholder="Title Post">
                                <div v-if="errors.title" class="alert alert-danger mt-2">
                                    <span>{{ errors.title[0] }}</span>
                                </div>
                            </div>
                            <div class="mb-3">
                                <label class="form-label fw-bold">Content</label>
                                <textarea class="form-control" v-model="content" rows="5" placeholder="Content Post"></textarea>
                                <div v-if="errors.content" class="alert alert-danger mt-2">
                                    <span>{{ errors.content[0] }}</span>
                                </div>
                            </div>
                            <button type="submit" class="btn btn-md btn-primary rounded-sm shadow border-0">Update</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>