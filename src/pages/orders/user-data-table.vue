<script setup lang="ts">
import { useHead } from '@vueuse/head'
import { useViewWrapper } from '/@src/stores/viewWrapper'
import { reactive, watchEffect } from "vue";
import { useApi } from '/@src/composable/useApi'

const viewWrapper = useViewWrapper()
viewWrapper.setPageTitle('User Data Table')
useHead({
    title: 'User Data Table - Components - Vuero',
})

const api = useApi()
let skip = ref(0)
let limit = ref(5)
const showLoader = ref(false)

interface UserType {
    firstName: string,
    age: number,
    birthDate: Date,
    phone: string,
    city: string,
    company: string
}

interface UserData {
    users: UserType[]
}

const usersData = reactive<UserData>({
    users: []
})

const columns = [
    { label: 'Name', field: 'firstName' },
    { label: 'Age', field: 'age', type: 'number' },
    { label: 'Date of birth', field: 'birthDate', type: 'date', dateInputFormat: 'yyyy-MM-dd', dateOutputFormat: 'do MMM yyyy' },
    { label: 'Mobile', field: 'phone', type: 'string' },
    { label: 'City', field: 'address.city', type: 'string' },
    { label: 'Company', field: 'company.name', type: 'string' },
]

const getUsersData = async (skip: number, limit: number): Promise<UserData> => {
    showLoader.value = true;
    let baseUrl = 'https://dummyjson.com/users';
    return await api.get(`${baseUrl}?skip=${skip}&limit=${limit}`)
}

watchEffect(() => {
    getUsersData(skip.value, limit.value).then((res: any) => {
        usersData.users = res.data.users
        showLoader.value = false;
    })
})

const onPageChange = (params: any): void => {
    skip.value += params.currentPerPage;
}

const onPerPageChange = (params: any): void => {
    skip.value = 0
    limit.value = params.currentPerPage
}

</script>

<template>
    <div class="page-content-inner">
        <VProgress v-if="!usersData.users.length || showLoader" size="tiny" color="info" />
        <vue-good-table v-if="usersData.users.length" :columns="columns" :rows="usersData.users"
            :pagination-options="{ enabled: true, perPage: 5, perPageDropdown: [5, 10, 20, 30] }"
            @page-change="onPageChange" @per-page-change="onPerPageChange" totalRows="100" theme="black-rhino" />
    </div>
</template>