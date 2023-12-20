<template>
  <div class="max-w-md mx-auto mt-8 p-6 bg-blue-900 rounded-md shadow-md">
    <h2 class="text-3xl text-white mb-4 font-semibold">Account Status Checker</h2>
    <form @submit.prevent="statusCheck">
      <div class="mb-4">
        <label for="email" class="block text-sm font-medium text-white">Email:</label>
        <input
          type="email"
          id="email"
          v-model="email"
          required
          class="mt-1 p-3 border border-white rounded-md w-full focus:outline-none focus:border-yellow-500 bg-blue-800 text-white"
        />
      </div>
      <button
        type="submit"
        class="bg-yellow-500 text-blue-900 p-3 rounded-md hover:bg-yellow-600 focus:outline-none focus:shadow-outline-yellow active:bg-yellow-800"
      >
        Check Status
      </button>
    </form>

    <div v-if="status !== null" class="mt-4">
      <h3 class="text-lg font-semibold text-white">Registration Status:</h3>
      <p class="mt-2 font-bold text-yellow-500">{{ status }}</p>
    </div>
  </div>
</template>

  
  <script>
  export default {
    data() {
      return {
        email: "",
        status: null,
      };
    },
    methods: {
      async statusCheck() {
        try {
          const apiUrl = `http://localhost:3100/api/data?email=${this.email}`;
          const response = await fetch(apiUrl, {
            method: "GET",
            headers: {
              "Content-Type": "application/json",
            },
          });
  
          if (response.ok) {
            const responseData = await response.json();
            console.log("API Response:", responseData);
  
            if (responseData.docs && responseData.docs.length > 0) {
              const userDocument = responseData.docs.find(
                (doc) => doc.email === this.email
              );
  
              if (userDocument) {
                this.status = userDocument.status;
              } else {
                console.error("Error: Email not found in the API response.");
              }
            } else {
              console.error("Error: No documents found in the API response.");
            }
          } else {
            console.error(
              "Failed to fetch status. Status code:",
              response.status
            );
          }
        } catch (error) {
          console.error("Error:", error);
        }
      },
    },
  };
  </script>
  