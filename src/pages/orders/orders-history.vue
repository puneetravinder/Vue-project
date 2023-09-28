<script setup lang="ts">
import { useHead } from '@vueuse/head'

import { useMarkdownToc } from '/@src/composable/useMarkdownToc'
import { useViewWrapper } from '/@src/stores/viewWrapper'

const markdownContainer = ref<HTMLElement>()
const toc = useMarkdownToc(markdownContainer)

const viewWrapper = useViewWrapper()
viewWrapper.setPageTitle('My Orders')

useHead({
    title: 'My Orders - Components - Vuero',
})
</script>

<template>
    <div class="page-content-inner">
        <h1>Orders history</h1>
    </div>
</template>