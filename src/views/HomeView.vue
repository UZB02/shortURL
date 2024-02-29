<template>
  <div class="container flex items-center h-screen justify-center gap-3 flex-col">
    <div class="container flex items-center justify-center">
      <form @submit.prevent="sendUrl" class="flex w-1/2">
        <input type="text" placeholder="url"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          v-model="url">
        <button type="submit"
          class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Create</button>
      </form>
    </div>
    <div class="card">
      <span>{{ shorturl }}</span>
      <!-- <span v-for="(item, key) in data.value" :key="key"  class="block max-w-sm p-6 bg-white border border-gray-200 rounded-lg shadow hover:bg-gray-100 dark:bg-gray-800 dark:border-gray-700 dark:hover:bg-gray-700">
  <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{{ respo  }}</h5>
  <p class="font-normal text-gray-700 dark:text-gray-400">Here are the biggest enterprise technology acquisitions of 2021 so far, in reverse chronological order.</p>
  </span> -->
    </div>
  </div>
</template>
<script setup>
import { reactive, ref } from 'vue'
import router from '@/router';
import axios from 'axios'
const url = ref('')
let shorturl = ref('')
let link = ref('')
const data = reactive({})
const sendUrl = async () => {
  if(!localStorage.getItem('token')){
    router.push('/login')
  }
  // let modifiedURL = url.value;
  for (let i = 0; i < url.value.length; i++) {
    if (url.value[i] === '/') {
      url.value = url.value.slice(0, i) + '%2F' + url.value.slice(i + 1);
    } else if (url.value[i] === ':') {
      url.value = url.value.slice(0, i) + '%3A' + url.value.slice(i + 1);
    }
    link.value = url.value
  }
console.log(link.value);


  let headersList = {
    "Authorization": `Bearer ${localStorage.getItem('token')}`,
    "Content-Type": "application/json"
  }

  let bodyContent = JSON.stringify({
    "link": link.value,
    "userid": `${localStorage.getItem('userid')}`,
  });

  let reqOptions = {
    url: "https://brogrammers.fn1.uz/api/ShortUrl/create",
    method: "POST",
    headers: headersList,
    data: bodyContent,
  }
  let response = await axios.request(reqOptions);
  console.log(response.data);
  shorturl.value=response.data
  // axios
  //   .get('https://brogrammers.fn1.uz/api/ShortUrl/get', {
  //     headers: {
  //       "Authorization": `Bearer ${localStorage.getItem('token')}`,
  //     }
  //   })
  //   .then(res => {
  //     categories.value = res.data.result
  //     console.log(res.data)
  //   })

}
</script>
<style scoped></style>