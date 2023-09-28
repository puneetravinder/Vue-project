<!-- <script setup lang="ts">
type TabId = 'interaction' | 'advanced'
const activeTab = ref<TabId>('interaction')
</script>

<template>
    <div class="navbar-subnavbar-inner tabs-wrapper">
        <div class="tabs-inner">
            <div class="tabs is-centered is-4">
                <ul>
                    <li :class="[activeTab === 'interaction' && 'is-active']">
                        <a tabindex="0" @keydown.space.prevent="activeTab = 'interaction'"
                            @click="activeTab = 'interaction'">Interaction</a>
                    </li>
                    <li :class="[activeTab === 'advanced' && 'is-active']">
                        <a tabindex="0" @keydown.space.prevent="activeTab = 'advanced'"
                            @click="activeTab = 'advanced'">Advanced</a>
                    </li>
                </ul>
            </div>
        </div>

        <div class="container">
            <div v-if="activeTab === 'interaction'" class="tab-content is-active">
                <div class="tab-content-inner">
                    <div class="center">
                        <div class="columns">
                            <div class="column is-3">
                                <h4 class="column-heading">My Orders</h4>
                                <ul>
                                    <li>
                                        <RouterLink to="/orders/current-orders">
                                            <i aria-hidden="true" class="lnil lnil-home"></i>
                                            <span>Current-order</span>
                                            <i aria-hidden="true" class="iconify" data-icon="feather:circle"></i>
                                        </RouterLink>
                                    </li>
                                    <li>
                                        <RouterLink to="/orders/orders-history">
                                            <i aria-hidden="true" class="lnil lnil-color-palette"></i>
                                            <span>Orders History</span>
                                            <i aria-hidden="true" class="iconify" data-icon="feather:circle"></i>
                                        </RouterLink>
                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
@import '/@src/scss/abstracts/all';
@import '/@src/scss/layout/navbar';
@import '/@src/scss/layout/responsive';
</style>
 -->