<script setup lang="ts">
import { useHead } from '@vueuse/head'

import { useViewWrapper } from '/@src/stores/viewWrapper'

const viewWrapper = useViewWrapper()
viewWrapper.setPageTitle('Current Orders')

useHead({
    title: 'Current Orders - Components - Vuero',
})
</script>

<template>
    <div class="page-content-inner">
        <h1>Current Orders</h1>
    </div>
</template>