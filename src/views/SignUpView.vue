<script setup>
import { RouterLink } from "vue-router";
import axios from "axios";
import { ref } from "vue";
import router from "@/router";
import { useAuthStore } from '@/stores/auth.store';

const email = ref("");
const username = ref("");
const password = ref("");
let loading = ref(false)

// const createUser = async (data) => {

//   // Perform data validation and cleaning


//   email.value = email.value.trim();
//   username.value = username.value.trim();
//   password.value = password.value.trim();


//   if (!email.value || !username.value || !password.value) {
//     console.log("Please fill in all fields.");
//     return;
//   }

//   // Send request to backend to create user
//   loading.value = true

//   try {
//     const response = await axios.post("http://127.0.0.1:8000/users/create_user", {
//       email: email.value,
//       username: username.value,
//       password: password.value,
//     });

//     // navigate to login page
//     router.push({
//       name: 'login',
//     })


//     console.log("User created successfully!");
//     // console.log(response.data);
//   } catch (error) {
//     loading.value = false
//     console.log("Error creating user. Please try again later.");
//     console.log(error);
//   }
// };


function createUser() {
  const authStore = useAuthStore();
  return authStore.signup(email.value, username.value, password.value)
    .catch(error => {
      console.log(error)
    });
}

</script>

<template>
  <section class="bg-gray-50 dark:bg-gray-900">
    <div class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0">
      <RouterLink to="/" class="flex items-center mb-6 text-2xl font-semibold text-gray-900 dark:text-white">
        <img class="w-25 h-25 mr-2" src="@/assets/logo.svg" alt="logo">
      </RouterLink>
      <div
        class="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700">
        <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
          <h1 class="text-xl font-bold leading-tight tracking-tight text-gray-900 md:text-2xl dark:text-white">
            Create and account
          </h1>

          <form class="space-y-4 md:space-y-6" method="POST">
            <div>
              <label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your
                email</label>
              <input v-model="email" type="email" name="email" id="email"
                class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="name@company.com" required>
            </div>
            <!-- <FormKit v-model="email" type="text" name="email" id="email" label="Email"
                    validation="required|email" placeholder="name@company.com" /> -->

            <div>
              <label for="username" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Your
                Name</label>
              <input v-model="username" type="text" name="username" id="username"
                class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="John Doe" required>
            </div>
            <!--
                                    <FormKit v-model="username" type="text" name="username" id="username" label="Username"
                                            validation="required" placeholder="John Doe" /> -->

            <div>
              <label for="password" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Password</label>
              <input v-model="password" type="password" name="password" id="password" placeholder="••••••••"
                class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                required>
            </div>

            <!-- <FormKit v-model="password" type="password" name="password" id="password" label="Password"
                    validation="required" placeholder="••••••••" /> -->


            <div class="flex items-start">
              <!-- <div class="flex items-center h-5">
                  <input v-model="termsAccepted" id="terms" aria-describedby="terms" type="checkbox" required
                      class="w-4 h-4 border border-gray-300 rounded bg-gray-50 focus:ring-3 focus:ring-primary-300 dark:bg-gray-700 dark:border-gray-600 dark:focus:ring-primary-600 dark:ring-offset-gray-800"
                      >
              </div> -->
              <div class="text-sm">
                <p class="font-light text-gray-500 dark:text-gray-300">I accept the
                  <RouterLink class="font-medium text-primary-600 hover:underline dark:text-primary-500"
                    to="terms-and-conditions">Terms and Conditions
                  </RouterLink>
                </p>
              </div>
            </div>
            <button type="button" @click="createUser" :disabled="loading"
              class="w-full text-white bg-primary-600 hover:bg-primary-700 focus:ring-4 focus:outline-none focus:ring-primary-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-primary-600 dark:hover:bg-primary-700 dark:focus:ring-primary-800">
              {{ loading ? "Please wait..." : "Create an account" }}
            </button>
            <p class="text-sm font-light text-gray-500 dark:text-gray-400">
              Already have an account?
              <RouterLink to="login" class="font-medium text-primary-600 hover:underline dark:text-primary-500">Login here
              </RouterLink>
            </p>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
</style>