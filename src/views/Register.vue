<template>
    <div class="w-full justify-center h-full bg-cyan-100 items-center mx-auto  py-20  px-2">
        <div class="max-w-xl mx-auto">
            <div class="bg-white p-5 shadow-lg rounded-lg flex flex-col">
                <div class="flex flex-col justify-center items-center">
                    <img src="/logo.png" class="w-1/2 text-center" alt="logo dmcode" style="margin-left: -18px;">
                    <p class="text-cyan-600 text-center font-semibold">
                        Daftarkan diri kamu, dan jadilah developer web yang hebat!
                    </p>

                </div>

                <form @submit.prevent="register" class="my-5 flex flex-col gap-y-5">
                    <div class="flex flex-col gap-y-2">
                        <p :class="validation.errors && validation.errors.name[0] ? 'text-red-500' : 'text-cyan-600'">
                            Nama
                        </p>
                        <div
                            :class="['flex', 'border-2', { 'border-red-500': validation.errors && validation.errors.name[0] }, 'border-cyan-600', 'rounded-lg']">
                            <input v-model="user.name" type="text"
                                class="flex-1 py-3 px-3 rounded-lg focus:outline-none" placeholder="nama lengkap">
                            <div class="p-3 flex-items-center">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 26 26">
                                    <path
                                        :fill="validation.errors && validation.errors.password[0] ? '#FF3131' : '#00a3af'"
                                        d="M16.563 15.9c-.159-.052-1.164-.505-.536-2.414h-.009c1.637-1.686 2.888-4.399 2.888-7.07c0-4.107-2.731-6.26-5.905-6.26c-3.176 0-5.892 2.152-5.892 6.26c0 2.682 1.244 5.406 2.891 7.088c.642 1.684-.506 2.309-.746 2.397c-3.324 1.202-7.224 3.393-7.224 5.556v.811c0 2.947 5.714 3.617 11.002 3.617c5.296 0 10.938-.67 10.938-3.617v-.811c0-2.228-3.919-4.402-7.407-5.557" />
                                </svg>
                            </div>
                        </div>
                        <p v-if="validation.errors && validation.errors.name" class="text-[11px] text-red-500 text-sm">
                            {{ validation.errors.name[0] }}</p>
                    </div>
                    <div class="flex flex-col gap-y-2">
                        <p :class="validation.errors && validation.errors.email[0] ? 'text-red-500' : 'text-cyan-600'">
                            Email
                        </p>
                        <div
                            :class="['flex', 'border-2', { 'border-red-500': validation.errors && validation.errors.email[0] }, 'border-cyan-600', 'rounded-lg']">
                            <input v-model="user.email" type="text"
                                class="flex-1 py-3 px-3 rounded-lg focus:outline-none" placeholder="email">
                            <div class="p-3 flex-items-center">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
                                    <path
                                        :fill="validation.errors && validation.errors.email[0] ? '#FF3131' : '#00a3af'"
                                        d="M20 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2m0 4l-8 5l-8-5V6l8 5l8-5z" />
                                </svg>
                            </div>
                        </div>
                        <p v-if="validation.errors && validation.errors.email" class="text-[11px] text-red-500 text-sm">
                            {{ validation.errors.email[0] }}</p>
                    </div>
                    <div class="flex flex-col gap-y-2">
                        <p
                            :class="validation.errors && validation.errors.password[0] ? 'text-red-500' : 'text-cyan-600'">
                            Password
                        </p>
                        <div
                            :class="['flex', 'border-2', { 'border-red-500': validation.errors && validation.errors.password[0] }, 'border-cyan-600', 'rounded-lg']">
                            <input v-model="user.password" :type="showPassword ? 'text' : 'password'"
                                class="flex-1 focus:outline-none py-3 px-3 rounded-lg" placeholder="password">
                            <span class="p-3 flex-items-center" @click="togglePasswordVisibility" v-if="!showPassword">

                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
                                    <path
                                        :fill="validation.errors && validation.errors.password[0] ? '#FF3131' : '#00a3af'"
                                        d="M12 9a3 3 0 0 0-3 3a3 3 0 0 0 3 3a3 3 0 0 0 3-3a3 3 0 0 0-3-3m0 8a5 5 0 0 1-5-5a5 5 0 0 1 5-5a5 5 0 0 1 5 5a5 5 0 0 1-5 5m0-12.5C7 4.5 2.73 7.61 1 12c1.73 4.39 6 7.5 11 7.5s9.27-3.11 11-7.5c-1.73-4.39-6-7.5-11-7.5" />
                                </svg>

                            </span>
                            <span class="p-3 flex-items-center" @click="togglePasswordVisibility" v-else>
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
                                    <path
                                        :fill="validation.errors && validation.errors.password[0] ? '#FF3131' : '#00a3af'"
                                        d="M14.33 7.17A15.642 15.642 0 0 0 12 7c-4.97 0-9 2.239-9 5c0 1.44 1.096 2.738 2.85 3.65l2.362-2.362a4 4 0 0 1 5.076-5.076zm-3.1 8.756a4 4 0 0 0 4.695-4.695l2.648-2.647C20.078 9.478 21 10.68 21 12c0 2.761-4.03 5-9 5c-.598 0-1.183-.032-1.749-.094zm6.563-10.719a1 1 0 1 1 1.414 1.414L6.48 19.35a1 1 0 1 1-1.414-1.414z" />
                                </svg>
                            </span>

                        </div>
                        <p v-if="validation.errors && validation.errors.password"
                            class="text-[11px] text-red-500 text-sm">
                            {{ validation.errors.password[0] }}</p>
                    </div>

                    <div class="flex flex-col gap-y-2">
                        <p
                            :class="validation.errors && validation.errors.password[0] ? 'text-red-500' : 'text-cyan-600'">
                            Konfirmasi Password
                        </p>
                        <div
                            :class="['flex', 'border-2', { 'border-red-500': validation.errors && validation.errors.password[0] }, 'border-cyan-600', 'rounded-lg']">
                            <input v-model="user.password_confirmation"
                                :type="showPasswordConfirmation ? 'text' : 'password'"
                                class="flex-1 focus:outline-none py-3 px-3 rounded-lg" placeholder="password">
                            <span class="p-3 flex-items-center" @click="togglePasswordConfirmationVisibility"
                                v-if="!showPasswordConfirmation">

                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
                                    <path
                                        :fill="validation.errors && validation.errors.password[0] ? '#FF3131' : '#00a3af'"
                                        d="M12 9a3 3 0 0 0-3 3a3 3 0 0 0 3 3a3 3 0 0 0 3-3a3 3 0 0 0-3-3m0 8a5 5 0 0 1-5-5a5 5 0 0 1 5-5a5 5 0 0 1 5 5a5 5 0 0 1-5 5m0-12.5C7 4.5 2.73 7.61 1 12c1.73 4.39 6 7.5 11 7.5s9.27-3.11 11-7.5c-1.73-4.39-6-7.5-11-7.5" />
                                </svg>

                            </span>
                            <span class="p-3 flex-items-center" @click="togglePasswordConfirmationVisibility" v-else>
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
                                    <path
                                        :fill="validation.errors && validation.errors.password[0] ? '#FF3131' : '#00a3af'"
                                        d="M14.33 7.17A15.642 15.642 0 0 0 12 7c-4.97 0-9 2.239-9 5c0 1.44 1.096 2.738 2.85 3.65l2.362-2.362a4 4 0 0 1 5.076-5.076zm-3.1 8.756a4 4 0 0 0 4.695-4.695l2.648-2.647C20.078 9.478 21 10.68 21 12c0 2.761-4.03 5-9 5c-.598 0-1.183-.032-1.749-.094zm6.563-10.719a1 1 0 1 1 1.414 1.414L6.48 19.35a1 1 0 1 1-1.414-1.414z" />
                                </svg>
                            </span>

                        </div>
                        <p v-if="validation.errors && validation.errors.password"
                            class="text-[11px] text-red-500 text-sm">
                            {{ validation.errors.password[0] }}</p>
                    </div>

                    <button class="bg-cyan-600 p-3 text-white font-semibold rounded-lg">
                        <p v-if="!loading" class="font-semibold text-white ">Daftar</p>
                        <p v-else class="font-semibold text-white ">Loading ...</p>
                    </button>

                    <div class="flex gap-x-3 items-center">
                        <div class="pt-[1px] w-full bg-cyan-600"></div>
                        <p class="text-cyan-600">Atau</p>
                        <div class="pt-[1px] w-full bg-cyan-600"></div>
                    </div>

                    <button
                        class="bg-white p-3 text-cyan-600 border-2 border-cyan-600 font-semibold rounded-lg flex gap-x-2 items-center justify-center hover:bg-gray-100"><svg
                            xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 128 128">
                            <path fill="#fff"
                                d="M44.59 4.21a63.28 63.28 0 0 0 4.33 120.9a67.6 67.6 0 0 0 32.36.35a57.13 57.13 0 0 0 25.9-13.46a57.44 57.44 0 0 0 16-26.26a74.3 74.3 0 0 0 1.61-33.58H65.27v24.69h34.47a29.72 29.72 0 0 1-12.66 19.52a36.2 36.2 0 0 1-13.93 5.5a41.3 41.3 0 0 1-15.1 0A37.2 37.2 0 0 1 44 95.74a39.3 39.3 0 0 1-14.5-19.42a38.3 38.3 0 0 1 0-24.63a39.25 39.25 0 0 1 9.18-14.91A37.17 37.17 0 0 1 76.13 27a34.3 34.3 0 0 1 13.64 8q5.83-5.8 11.64-11.63c2-2.09 4.18-4.08 6.15-6.22A61.2 61.2 0 0 0 87.2 4.59a64 64 0 0 0-42.61-.38" />
                            <path fill="#e33629"
                                d="M44.59 4.21a64 64 0 0 1 42.61.37a61.2 61.2 0 0 1 20.35 12.62c-2 2.14-4.11 4.14-6.15 6.22Q95.58 29.23 89.77 35a34.3 34.3 0 0 0-13.64-8a37.17 37.17 0 0 0-37.46 9.74a39.25 39.25 0 0 0-9.18 14.91L8.76 35.6A63.53 63.53 0 0 1 44.59 4.21" />
                            <path fill="#f8bd00"
                                d="M3.26 51.5a63 63 0 0 1 5.5-15.9l20.73 16.09a38.3 38.3 0 0 0 0 24.63q-10.36 8-20.73 16.08a63.33 63.33 0 0 1-5.5-40.9" />
                            <path fill="#587dbd"
                                d="M65.27 52.15h59.52a74.3 74.3 0 0 1-1.61 33.58a57.44 57.44 0 0 1-16 26.26c-6.69-5.22-13.41-10.4-20.1-15.62a29.72 29.72 0 0 0 12.66-19.54H65.27c-.01-8.22 0-16.45 0-24.68" />
                            <path fill="#319f43"
                                d="M8.75 92.4q10.37-8 20.73-16.08A39.3 39.3 0 0 0 44 95.74a37.2 37.2 0 0 0 14.08 6.08a41.3 41.3 0 0 0 15.1 0a36.2 36.2 0 0 0 13.93-5.5c6.69 5.22 13.41 10.4 20.1 15.62a57.13 57.13 0 0 1-25.9 13.47a67.6 67.6 0 0 1-32.36-.35a63 63 0 0 1-23-11.59A63.7 63.7 0 0 1 8.75 92.4" />
                        </svg>
                        <p>Daftar dengan google</p>
                    </button>

                    <div class="flex justify-center items-center">
                        <p class="text-cyan-600">
                            Sudah punya akun ? <router-link :to="{ name: 'login' }" class="font-semibold">masuk
                            </router-link>
                        </p>




                    </div>
                </form>
            </div>


        </div>
    </div>
</template>

<script>
import { ref, reactive } from 'vue'
import { useStore } from 'vuex'
import { useToast } from "vue-toastification"
//hook vue router
import { useRouter } from 'vue-router'


export default {

    name: 'RegisterComponent',

    setup() {

        const password = ref('');
        const showPassword = ref(false);
        const showPasswordConfirmation = ref(false);
        const loading = ref(false);

        // Methods
        const togglePasswordVisibility = () => {

            showPassword.value = !showPassword.value;
        };

        const togglePasswordConfirmationVisibility = () => {

            showPasswordConfirmation.value = !showPasswordConfirmation.value;
        };

        //user state
        const user = reactive({
            name: '',
            email: '',
            password: '',
            password_confirmation: ''
        })

        //validation state
        const validation = ref([])
        const store = useStore()

        //route
        const router = useRouter()
        const toast = useToast()
        function register() {

            loading.value = true;
            //define variable 
            let name = user.name
            let email = user.email
            let password = user.password
            let password_confirmation = user.password_confirmation

            //panggil actions "register" dari module "auth"
            store.dispatch('auth/register', {
                name,
                email,
                password,
                password_confirmation
            })
                .then(() => {

                    //redirect ke dashboard
                    router.push({ name: 'login' })
                    toast.success("Register Berhasil!, cek email untuk verifikasi akun")

                }).catch(error => {

                    //show validaation message
                    // validation.value = error;
                    validation.value = error;
                    loading.value = false;
                    if (validation.value.message) {
                        toast.error(`${validation.value.message}`)
                    }

                })
        }


        //return object
        return {

            password,
            showPassword,
            togglePasswordVisibility,
            togglePasswordConfirmationVisibility,
            user,
            validation,
            showPasswordConfirmation,
            loading,
            register,
            toast
        }

    }

}
</script>