<script setup lang="ts">
const emit = defineEmits(['close'])
</script>

<template>
    <div class="sidebar-panel is-generic">
        <div class="subpanel-header">
            <h3 class="no-mb">My Orders</h3>
            <div class="panel-close" tabindex="0" @keydown.space.prevent="emit('close')" @click="emit('close')">
                <i aria-hidden="true" class="iconify" data-icon="feather:x"></i>
            </div>
        </div>
        <div class="inner" data-simplebar>
            <ul>
                <li>
                    <RouterLink to="/orders/current-orders">Current Order</RouterLink>
                </li>
                <li>
                    <RouterLink to="/orders/orders-history">Orders History</RouterLink>
                </li>
                <li class="divider with-label">
                    <span class="divider-label">Posts Data</span>
                </li>
                <li>
                    <RouterLink to="/orders/user-posts">User Posts</RouterLink>
                </li>
                <li>
                    <RouterLink to="/orders/user-data-table">User Data Table</RouterLink>
                </li>
            </ul>
        </div>
    </div>
</template>

<style lang="scss">
@import '/@src/scss/layout/sidebar-panel';
</style>
