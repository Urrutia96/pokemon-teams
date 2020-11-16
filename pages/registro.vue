<template>
  <div
    class="flex flex-col sm:justify-center items-center pt-6 sm:pt-0 bg-gray-100"
  >
    <div>
      <a href="/">
        <img src="/img/logo.svg" class="w-20 h-20 fill-current text-gray-500" />
      </a>
    </div>

    <div
      class="w-full sm:max-w-md mt-6 px-6 py-4 bg-white shadow-md overflow-hidden sm:rounded-lg"
    >
      <!-- Session Status -->

      <!-- Validation Errors -->

      <form @submit.prevent="submit">
        <input
          type="hidden"
          name="_token"
          value="Yq6MK4lZbXI93kS6ZLIYJ7QkAglEcoC057fickhR"
        />
        <!-- Email Address -->
        <div>
          <label class="block font-medium text-sm text-gray-700" for="name">
            Nombre
          </label>

          <input
            class="form-input rounded-md shadow-sm block mt-1 w-full"
            id="name"
            type="text"
            v-model="form.name"
            required="required"
            autofocus="autofocus"
          />
        </div>

        <div>
          <label class="block font-medium text-sm text-gray-700" for="email">
            Email
          </label>

          <input
            class="form-input rounded-md shadow-sm block mt-1 w-full"
            id="email"
            type="email"
            v-model="form.email"
            required="required"
          />
        </div>

        <!-- Password -->
        <!-- <div class="mt-4">
          <label class="block font-medium text-sm text-gray-700" for="password">
            Password
          </label>

          <input
            class="form-input rounded-md shadow-sm block mt-1 w-full"
            id="password"
            type="password"
            name="password"
            required="required"
            autocomplete="current-password"
          />
        </div> -->

        <div class="flex items-center justify-end mt-4">
          <button
            type="submit"
            class="inline-flex items-center px-4 py-2 bg-gray-800 border border-transparent rounded-md font-semibold text-xs text-white uppercase tracking-widest hover:bg-gray-700 active:bg-gray-900 focus:outline-none focus:border-gray-900 focus:shadow-outline-gray disabled:opacity-25 transition ease-in-out duration-150 ml-3"
          >
            Login
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form:{
        name: '',
        email: ''
      }
    }
  },
  methods: {
    submit(){
      localStorage.setItem('user', JSON.stringify(this.form))
      this.$router.push('/')
    }
  }
};
</script>

<style>
</style>