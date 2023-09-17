<script setup lang="ts">
 import { Response } from 'node-fetch'; // Add this import

    //meta title
    useHead({
        title: 'Create a Notes - Isam Samsul Arip',
    });

    // init config
    const config = useRuntimeConfig();

    // init router
    const router = useRouter();

    // define state
    const title = ref('');
    const content = ref('');
    const errors: any = ref({});

    // method "storePost"
    const storePost = async () => {
    if (!title.value || !content.value) {
        errors.value = {
            title: ['Title is required'],
            content: ['Content is required'],
        };
        return; // Stop further execution if validation fails
    }
    try {
        const response: Response = await $fetch(`${config.public.apiBase}/api/notes`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({
                title: title.value,
                content: content.value,
            }),
        });
        router.push({ path: "/posts" });

    } catch (error) {
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
                        <form @submit.prevent="storePost()">
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
                            <button type="submit" class="btn btn-md btn-primary rounded-sm shadow border-0">Save</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>