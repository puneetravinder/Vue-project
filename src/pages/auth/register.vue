<script setup lang="ts">
import { reactive, watch } from "vue";
import useVuelidate from '@vuelidate/core'
import {
    required, maxLength, minLength,
    numeric, between, helpers
} from '@vuelidate/validators'

const alphaNumWithSpace = helpers.regex(/^[a-zA-Z\d\s]+$/);
const alphaWithSpace = helpers.regex(/^[a-zA-Z\s]+$/);
const mobileNumberStartWith = helpers.regex(/^(6|7|8|9)/);

const isBtnDisabled = ref(true)
const formSubmitted = ref(false)
let userValues = ref()

interface UserData {
    firstName: string,
    lastName: string,
    age: number | undefined,
    mobile: number | undefined,
    alternateMobile?: number | undefined,
    address: string,
    gender: string
}

let initialState = {
    firstName: '',
    lastName: '',
    age: undefined,
    mobile: undefined,
    alternateMobile: undefined,
    address: '',
    gender: ''
}

const userData = reactive({ ...initialState });

const notSameAsMobile = () => {
    if (userData.mobile === userData.alternateMobile) return false
    return true
}

const rules = computed(() => {
    return {
        firstName: {
            required: helpers.withMessage('First name is required', required),
            alphaWithSpace: helpers.withMessage('The value is not alphabetical', alphaWithSpace),
            maxLength: maxLength(15)
        },
        lastName: {
            required: helpers.withMessage('Last name is required', required),
            alphaWithSpace: helpers.withMessage('The value is not alphabetical', alphaWithSpace),
            maxLength: maxLength(15)
        },
        age: {
            required: helpers.withMessage('Age is required', required),
            numeric,
            between: between(19, 100),
        },
        mobile: {
            required: helpers.withMessage('Mobile number is required', required),
            numeric,
            minLength: minLength(10),
            maxLength: maxLength(10),
            mobileNumberStartWith: helpers.withMessage('Mobile number series should only start with 6/7/8/9', mobileNumberStartWith)
        },
        alternateMobile: {
            numeric,
            minLength: minLength(10),
            maxLength: maxLength(10),
            notSameAsMobile: helpers.withMessage('Alternate mobile number should be different', notSameAsMobile),
            mobileNumberStartWith: helpers.withMessage('Altername mobile number series should only start with 6/7/8/9', mobileNumberStartWith)
        },
        address: {
            required: helpers.withMessage('Address is required', required),
            alphaNumWithSpace: helpers.withMessage('The value should be alpha numeric only', alphaNumWithSpace)
        },
        gender: { required: helpers.withMessage('Please select a gender', required) }
    }
})

const v$ = useVuelidate(rules, userData)

const handleSignup = async () => {
    const result = await v$.value.$validate()
    if (result) {
        resetForm()
        formSubmitted.value = true;
    }
}

const resetForm = () => {
    Object.assign(userValues, userData);
    Object.assign(userData, initialState);
    v$.value.$reset()
}

watch(userData, () => {
    isBtnDisabled.value = true;
    if (userData.firstName !== "" && userData.lastName !== "" && userData.age
        && userData.mobile && userData.address !== "" && userData.gender !== "") {
        isBtnDisabled.value = false;
    }
})

</script>

<template>
    <VCard v-if="formSubmitted">
        <h3 class="title is-2 mb-2">User Details</h3>
        <p>First Name : {{ userValues?.firstName }}</p>
        <p>Last Name : {{ userValues?.lastName }}</p>
        <p>Age : {{ userValues?.age }}</p>
        <p>Mobile Number : {{ userValues?.mobile }}</p>
        <p v-if="userValues?.alternateMobile">Alternate mobile number : {{ userValues?.alternateMobile }}</p>
        <p>Address : {{ userValues?.address }}</p>
        <p>Gender : {{ userValues?.gender }}</p>
    </VCard>
    <div class="auth-wrapper-inner is-single">
        <div class="single-form-wrap">
            <div class="inner-wrap">
                <div class="auth-head">
                    <h2>New User Registeration</h2>
                </div>
                <!--Form-->
                <div class="form-card">
                    <form @submit.prevent="handleSignup">
                        <div class="login-form">
                            <VField label="First Name">
                                <VControl fullwidth>
                                    <VInput v-model="userData.firstName" type="text" placeholder="Enter first name" />
                                    <p v-for="(error, index) of v$.firstName.$errors" :key="index" class="help is-danger">
                                        {{ error.$message }}
                                    </p>
                                </VControl>
                            </VField>
                            <VField label="Last Name">
                                <VControl fullwidth>
                                    <VInput v-model="userData.lastName" type="text" placeholder="Enter last name" />
                                    <p v-for="(error, index) of v$.lastName.$errors" :key="index" class="help is-danger">
                                        {{ error.$message }}
                                    </p>
                                </VControl>
                            </VField>
                            <VField label="Age">
                                <VControl>
                                    <VInput v-model.number="userData.age" type="number" placeholder="Enter you age"
                                        autocomplete="age" />
                                    <p v-for="(error, index) of v$.age.$errors" :key="index" class="help is-danger">
                                        {{ error.$message }}
                                    </p>
                                </VControl>
                            </VField>
                            <VField label="Mobile Number">
                                <VControl>
                                    <VInput v-model.number="userData.mobile" type="number" placeholder="Enter mobile number"
                                        autocomplete="mobile" />
                                    <p v-for="(error, index) of v$.mobile.$errors" :key="index" class="help is-danger">
                                        {{ error.$message }}
                                    </p>
                                </VControl>
                            </VField>
                            <VField label="Altername Mobile Number">
                                <VControl>
                                    <VInput v-model.number="userData.alternateMobile" type="number"
                                        placeholder="Enter alternate number (optional)" autocomplete="mobile" />
                                    <p v-for="(error, index) of v$.alternateMobile.$errors" :key="index"
                                        class="help is-danger">
                                        {{ error.$message }}
                                    </p>
                                </VControl>
                            </VField>
                            <VField label="Parmanent Address">
                                <VControl>
                                    <VTextarea v-model="userData.address" rows="2"
                                        placeholder="Enter your parmanent address">
                                    </VTextarea>
                                    <p v-for="(error, index) of v$.address.$errors" :key="index" class="help is-danger">
                                        {{ error.$message }}
                                    </p>
                                </VControl>
                            </VField>
                            <VField label="Gender">
                                <VControl>
                                    <VRadio v-model="userData.gender" value="male" label="Male" name="outlined_radio"
                                        color="primary" />
                                    <VRadio v-model="userData.gender" value="female" label="Female" name="outlined_radio"
                                        color="primary" />
                                    <p v-for="(error, index) of v$.gender.$errors" :key="index" class="help is-danger">
                                        {{ error.$message }}
                                    </p>
                                </VControl>
                            </VField>
                            <div class="login">
                                <VButton :disabled="isBtnDisabled" color="info" type="submit" bold fullwidth raised>
                                    Sign Up
                                </VButton>
                            </div>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>