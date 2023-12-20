<template>
  <section class="bg-gray-100 dark:bg-gray-900">
    <div class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0">
      <div
        class="w-full bg-white rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 dark:bg-gray-800 dark:border-gray-700">
        <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
          <div class="flex items-center justify-center">
            <h1 class="text-2xl font-bold leading-tight tracking-tight text-gray-800 md:text-3xl dark:text-white">
              Register Your Data
            </h1>
          </div>
          <form @submit.prevent="registerAcc" class="space-y-4 md:space-y-6" action="#">
            <div>
              <label for="name" class="block mb-2 text-sm font-medium text-gray-800 dark:text-white">Your Name</label>
              <input v-model="name" type="text" name="name" id="name" ref="name"
                class="bg-gray-100 border border-gray-300 text-gray-800 sm:text-sm rounded-lg focus:ring-indigo-500 focus:border-indigo-500 block w-full p-3 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-indigo-500 dark:focus:border-indigo-500"
                placeholder="Etha Felisya" required />
            </div>
            <div>
              <label for="email" class="block mb-2 text-sm font-medium text-gray-800 dark:text-white">Your Email</label>
              <input v-model="email" type="email" name="email" id="email" ref="email" placeholder="etha@mail.com"
                class="bg-gray-100 border border-gray-300 text-gray-800 sm:text-sm rounded-lg focus:ring-indigo-500 focus:border-indigo-500 block w-full p-3 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-indigo-500 dark:focus:border-indigo-500"
                required />
            </div>
            <div>
              <label for="school" class="block mb-2 text-sm font-medium text-gray-800 dark:text-white">Your School</label>
              <input v-model="sekolah" type="text" name="school" id="school" ref="school" placeholder="Sman Saka"
                class="bg-gray-100 border border-gray-300 text-gray-800 sm:text-sm rounded-lg focus:ring-indigo-500 focus:border-indigo-500 block w-full p-3 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-indigo-500 dark:focus:border-indigo-500"
                required />
            </div>
            <button type="submit"
              class="w-full text-white bg-indigo-600 hover:bg-indigo-900 focus:ring-4 focus:outline-none focus:ring-indigo-300 font-medium rounded-lg text-sm px-5 py-3 text-center dark:bg-indigo-600 dark:hover:bg-indigo-700 dark:focus:ring-indigo-800">
              Register now
            </button>
            <p class="text-sm font-light text-gray-600 dark:text-gray-400">
              Already have an account? <NuxtLink to="/login"
                class="font-medium text-indigo-600 hover:underline dark:text-indigo-500">Login here</NuxtLink>
            </p>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

 <script>  
export default {
  data() {
    return {
      name: '',
      email: '',
      sekolah: ''
    };
  },
  methods: {
    async registerAcc() {
      try {
        const apiUrl = 'http://localhost:3100/api/Data/';

        const response = await fetch(apiUrl, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            namaPanjang: this.name,
            email: this.email,
            asalSekolah: this.sekolah,
          })
        });

        if (response.ok) {
          const responseData = await response.json();
          if (responseData) {
            alert('Registration Complete');
            // Optionally, reset form fields after successful registration
            this.name = '';
            this.email = '';
            this.sekolah = '';
          }
        } else {
          // Handle non-successful response
          console.error('Registration failed:', response.statusText);
          alert('Error occurred while registering data');
        }
      } catch (error) {
        console.error('Error occurred:', error);
        alert('Error occurred while registering data');
      }
    }
  }
};

</script> 
