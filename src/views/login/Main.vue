<template>
    <section class="bg-gray-50 h-screen dark:bg-gray-900">
        <div class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0">
            <div
                class="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700">
                <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
                    <h1 class="text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl dark:text-white">
                      Log In
                    </h1>
                    <form class="space-y-4 md:space-y-6" action="#">
                        <div>
                            <label for="emailAddress"
                                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your Email</label>
                            <input type="email" v-model="emailAddress" name="emailAddress" id="emailAddress"
                                placeholder="jhonwuck@gmail.com"
                                class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                                required="">
                        </div>
                        <div>
                            <label for="password"
                                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Password</label>
                            <input type="password" v-model="password" name="password" id="password" placeholder="••••••••"
                                class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                                required="">
                        </div>
                        <button type="submit" @click="handleSubmit"
                            class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800">Log IN</button>
                        <p class="text-sm font-light text-gray-500 dark:text-gray-400">
                            Don't have an account? <a @click="aboutpage" href="#"
                                class="font-medium text-primary-600 hover:underline dark:text-primary-500">Register</a>
                        </p>
                    </form>
                </div>
            </div>
        </div>
    </section>
</template>
<script setup>
import { ref, toRaw } from 'vue';
import axios from 'axios'
import router from '@/router';

const emailAddress = ref('');
const password = ref('');

const handleSubmit = async (e) => {
    e.preventDefault();
    const data = {
        emailAddress: emailAddress.value,
        password: password.value,
    };
    console.log(toRaw(data));

    try {
        axios.post('https://brogrammers.fn1.uz/api/Authentication/login-user', data)
            .then(function (response) {

                if (response.status === 200) {
                    router.push('/');
                    const token = response.data.token // Tokenni olish
                    const userid = response.data.userId
                    localStorage.setItem('token', token)
                    localStorage.setItem('userid', userid)
                    console.log(response.data.token);
                }
            })
    } catch (error) {
        console.error(error);
    }
};

const aboutpage = () => {
    router.push('/register');
}

</script>
<style></style>
