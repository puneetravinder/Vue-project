<script setup lang="ts">
import { useHead } from '@vueuse/head'
import { useViewWrapper } from '/@src/stores/viewWrapper'
import { reactive, watchEffect } from "vue";
import { useRouter } from "vue-router";
import { useApi } from '/@src/composable/useApi'

const viewWrapper = useViewWrapper()
viewWrapper.setPageTitle('User Posts')
useHead({
    title: 'Posts - Components - Vuero',
})
const api = useApi();
let limit = 10;
const router = useRouter()

interface Post {
    userId: number,
    id: number,
    title: string,
    body: string
}

interface PostData {
    posts: Post[]
}

let postData = reactive<PostData>({
    posts: []
})

const getData = (): void => {
    getPosts(limit).then((res: any) => {
        postData.posts = res.data
    })
}

const getPosts = async (limit: number): Promise<Post> => {
    let baseUrl = 'https://jsonplaceholder.typicode.com/posts?_limit=';
    return await api.get(`${baseUrl}${limit}`)
}

watchEffect(() => {
    getData()
})

const loadMorePosts = () => {
    limit += 10
    getData()
}

const handlePostClick = (postId: number) => {
    router.push(`/orders/user-posts/${postId}`)
}

</script>

<template>
    <div class="page-content-inner">
        <VProgress v-if="!postData.posts.length" size="tiny" color="info" />
        <div v-if="postData.posts.length" class="mb-3">
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));grid-gap: 5px;">
                <div v-for="post in postData.posts" :key="post?.id" class="m-1 has-text-left">
                    <VCard @click="handlePostClick(post.id)" radius="rounded" color="info" class="is-clickable my-3"
                        style="height: 100%;" elevated>
                        <h3 class="title is-5 mb-2">{{ post?.title }}</h3>
                        <p>{{ post?.body }}</p>
                    </VCard>
                </div>
            </div>
        </div>
        <VButton v-if="postData.posts.length" @click="loadMorePosts" class="is-pulled-right mt-2" color="info" raised
            outlined> Load more... </VButton>
    </div>
</template>