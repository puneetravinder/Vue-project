<script setup lang="ts">
import { useHead } from '@vueuse/head'
import { useViewWrapper } from '/@src/stores/viewWrapper'
import { reactive, watchEffect } from "vue";
import { RouteRecordNormalized, useRoute } from "vue-router";
import { useApi } from '/@src/composable/useApi'

const viewWrapper = useViewWrapper()
viewWrapper.setPageTitle('Post Comments')
useHead({
    title: 'Post Comments - Components - Vuero',
})

interface ParamsTypes {
    postId: string;
}

interface CustomRoute {
    path: string;
    params: ParamsTypes;
    query: Record<string, string | string[]>;
    fullPath: string;
    matched: RouteRecordNormalized[];
    // Add any other properties you want to access from the route object
}

const route = useRoute() as CustomRoute;
const api = useApi();
const breadcrumb = [
    {
        label: 'User Posts',
        hideLabel: true,
        to: '/orders/user-posts',
    },
    {
        label: 'Post Comments'
    }
]

interface Comment {
    postId: number,
    id: number,
    name: string,
    email: string,
    body: string
}

interface CommentData {
    comments: Comment[]
}

let commentData = reactive<CommentData>({
    comments: []
})

const getComments = async (): Promise<Comment> => {
    let id = route.params.postId;
    let baseUrl = 'https://jsonplaceholder.typicode.com/posts/';
    return await api.get(`${baseUrl}${id}/comments`)
}

watchEffect(() => {
    getComments().then((res: any) => {
        commentData.comments = res.data
    })
})

</script>

<template>
    <div class="page-content-inner">
        <VBreadcrumb :items="breadcrumb" />
        <VProgress v-if="!commentData.comments.length" size="tiny" color="info" />
        <div v-if="commentData.comments.length">
            <div class="columns is-multiline is-gap">
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));grid-gap: 5px;">
                    <div v-for="comment in commentData.comments" :key="comment?.id" class="m-1">
                        <VCard radius="rounded" elevated style="height: 100%;">
                            <div class="card-head">
                                <VBlock :title="comment.name" :subtitle="comment.email" center class="no-margin">
                                    <template #icon>
                                        <Tippy class="has-help-cursor" interactive :offset="[0, 10]" placement="top-start">
                                            <VAvatar picture="/images/avatars/svg/vuero-1.svg"
                                                badge="/images/icons/flags/germany.svg" />
                                        </Tippy>
                                    </template>
                                </VBlock>
                            </div>
                            <div class="card-inner">
                                <p>{{ comment.body }}</p>
                            </div>
                        </VCard>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
  