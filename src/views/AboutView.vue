<template>
  <section class="bg-gray-50 dark:bg-gray-900">
    <div class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0">
      <div
        class="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700">
        <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
          <h1 class="text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl dark:text-white">
            Create and account
          </h1>
          <form class="space-y-4 md:space-y-6" action="#">
            <div>
              <label for="firstName" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">First
                Name</label>
              <input type="text" v-model="firstName" name="firstName" id="firstName" placeholder="Jhon"
                class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                required="">
            </div>
            <div>
              <label for="lastName" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Last Name</label>
              <input type="text" v-model="lastName" name="lastName" id="lastName" placeholder="Jhon"
                class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                required="">
            </div>
            <div>
              <label for="userName" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Last Name</label>
              <input type="text" v-model="userName" name="userName" id="userName" placeholder="Jeack"
                class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                required="">
            </div>
            <div>
              <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your email</label>
              <input type="email" v-model="email" name="email" id="email"
                class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="name@company.com" required="">
            </div>
            <div>
              <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Password</label>
              <input type="password" v-model="password" name="password" id="password" placeholder="••••••••"
                class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                required="">
            </div>
            <button type="submit" @click="handleSubmit"
              class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800">Create
              an account</button>
            <p class="text-sm font-light text-gray-500 dark:text-gray-400">
              Already have an account? <a href="http://localhost:5173"
                class="font-medium text-primary-600 hover:underline dark:text-primary-500">Login here</a>
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

const firstName = ref('');
const lastName = ref('');
const email = ref('');
const password = ref('');
const userName = ref(null);

const handleSubmit = async (e) => {
  e.preventDefault();
  const data = {
    firstName: firstName.value,
    lastName: lastName.value,
    emailAddress: email.value,
    password: password.value,
    userName: userName.value
  };
  console.log(toRaw(data));

  try {
    axios.post('https://brogrammers.fn1.uz/api/Authentication/register-user', data)
      .then(function (response) {
        console.log(response, 66666);

        if (response.status === 200) {
          // 200 status kodi qaytganida "about" sahifaga yo'naltiruvchi kodni qo'shing
          // window.location.href = '/about';
          router.push('/login');
        }
      })
  } catch (error) {
    console.error(error);
  }
};

</script>
