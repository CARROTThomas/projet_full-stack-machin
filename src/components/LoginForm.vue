<script setup lang="ts">
import { ref } from 'vue';
import axios from "axios";
import router from "@/router";

const email = ref('');
const password = ref('');

const handleSubmit = async () => {
  console.log('Email:', email.value);
  console.log('Password:', password.value);
  try {
    const response = await login();
    localStorage.setItem('bearerToken', response.data.token);
    window.location.reload();
    await router.push('/profile');
  } catch (error) {
    console.error("Erreur lors du login :", error);
  }
};

const login = async () => {
  const url = "https://fsapi.thibautstachnick.com";
  try {
    const response = await axios.post(`${url}/api/login_check`, {
      email: email.value,
      password: password.value
    });
    localStorage.setItem('bearerToken', response.data.token);
    return response;
  } catch (error) {
    console.error("Erreur lors de la requête POST :", error);
    throw error;
  }
};

</script>

<template>
  <div class="flex justify-center">
    <img src="../assets/logo1.png" alt="logo" class="logo-register" height="66" width="97" />
  </div>
  <div class="flex justify-center">
    <h1 class="h1-css">Login</h1>
  </div>

  <form class="max-w-sm mx-auto" @submit.prevent="handleSubmit">
    <div class="mb-5 input-div">
      <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Email</label>
      <input type="email" id="email" v-model="email" class="input-text bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="name@flowbite.com" required />
    </div>
    <div class="mb-5">
      <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Password</label>
      <input type="password" id="password" v-model="password" class="input-text bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="password" required />
    </div>
    <div class="flex justify-center div-button-form">
      <button type="submit" class="submit-button text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">Submit</button>
    </div>
    <div class="flex justify-center">
      <p class="span-login-form">Create an account ? <router-link class="" to="/register">Sign up</router-link>
      </p>
    </div>
  </form>
</template>


<style scoped>

.h1-css{
  font-size: 50px;
  font-family: "Work Sans", sans-serif;
  padding-bottom: 100px;
}
.submit-button{
  width: max-content;
}
.input-text{
  color: white;
  background: #6E7DAB;
}
.input-div{
  color: white;
  padding-bottom: 25px;
}
.div-button-form{
  padding-top: 50px;
  padding-bottom: 25px;
}
.div-button-form{
  font-size: 10px;
  color: #252525;
}
::placeholder {
  color: white;
  opacity: 0.3; /* Firefox */
}
::-ms-input-placeholder { /* Edge 12 -18 */
  color: white;
}
.submit-button{
  background: #6E7DAB;
}
.logo-register{
  padding-bottom: 25px;
  padding-top: 25px;
}
</style>
