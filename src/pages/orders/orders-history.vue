<script setup lang="ts">
import { useHead } from '@vueuse/head'
import { useViewWrapper } from '/@src/stores/viewWrapper'

const viewWrapper = useViewWrapper()
viewWrapper.setPageTitle('Orders History')

useHead({
    title: 'Orders History - Orders - Vuero',
})
</script>

<template>
    <div class="page-content-inner">
        <h1>Orders history</h1>
    </div>
</template>