<template>
  <div>
    <div class="h-2 w-full bg-red-600"></div>
    <div class="relative bg-white shadow">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 container">
        <div
          class="flex justify-between items-center border-b-2 border-gray-100 py-3 md:justify-start md:space-x-10"
        >
          <div class="lg:w-0 lg:flex-1">
            <a href="#" class="flex">
              <img
                class="h-8 w-auto sm:h-10"
                src="/img/logo.svg"
                alt="Workflow"
              />
            </a>
          </div>
          <div class="-mr-2 -my-2 md:hidden">
            <button
            @click="toggleMenu"
              type="button"
              class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-gray-500 hover:bg-gray-100 focus:outline-none focus:bg-gray-100 focus:text-gray-500 transition duration-150 ease-in-out"
            >
              <!-- Heroicon name: menu -->
              <svg
                class="h-6 w-6"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M4 6h16M4 12h16M4 18h16"
                />
              </svg>
            </button>
          </div>
          <nav class="hidden md:flex space-x-10">
            <nuxt-link
              v-for="option in menuOptions" :key="option.label" 
              :to="option.link"
              exact-active-class="text-red-600"
              exact-active-class.remove="text-gray-500"
              class="text-lg leading-6 font-medium text-gray-500 hover:text-red-700 focus:outline-none focus:text-red-700 transition ease-in-out duration-150"
            >
              {{option.label}}
            </nuxt-link>
          </nav>
          <div
            class="hidden md:flex items-center justify-end space-x-8 md:flex-1 lg:w-0"
          >
            <span v-if="user"
              class="whitespace-no-wrap text-lg leading-6 font-medium text-gray-500 hover:text-gray-900 focus:outline-none focus:text-gray-900"
            >
              {{ user.name }}
            </span>
            <span class="inline-flex rounded-md shadow-sm">
              <div v-if="!user">
                <nuxt-link
                  to="/registro"
                  class="whitespace-no-wrap inline-flex items-center justify-center px-4 py-2 border border-transparent text-lg leading-6 font-medium rounded-md text-white bg-red-600 hover:bg-red-500 focus:outline-none focus:border-red-700 focus:shadow-outline-red active:bg-red-700 transition ease-in-out duration-150"
                >
                  Registro
                </nuxt-link>
              </div> 
              <div v-if="user">
                <button
                  class="whitespace-no-wrap inline-flex items-center justify-center px-4 py-2 border border-transparent text-lg leading-6 font-medium rounded-md text-white bg-red-600 hover:bg-red-500 focus:outline-none focus:border-red-700 focus:shadow-outline-red active:bg-red-700 transition ease-in-out duration-150"
                >
                  Eliminar Cuenta
                </button>
              </div>
            </span>
          </div>
        </div>
      </div>

      <transition
        enter-active-class="transition duration-200 ease-out transform"
        enter-class="opacity-0 scale-95"
        enter-to-class="opacity-100 scale-100"
        leave-active-class="transition ease-in duration-75 transform"
        leave-class="opacity-100 scale-100"
        leave-to-class="opacity-0 scale-95"
        >
        <div
          class="absolute top-0 inset-x-0 p-2 transition transform origin-top-right md:hidden"
          v-show="isOpen"
        >
          <div class="rounded-lg shadow-lg">
            <div class="rounded-lg shadow-xs bg-white divide-y-2 divide-gray-50">
              <div class="pt-5 pb-6 px-5 space-y-6">
                <div class="flex items-center justify-between">
                  <div>
                    <img
                      class="h-8 w-auto"
                      src="/img/logo.svg"
                      alt="Workflow"
                    />
                  </div>
                  <div class="-mr-2">
                    <button
                      @click="toggleMenu"
                      type="button"
                      class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-gray-500 hover:bg-gray-100 focus:outline-none focus:bg-gray-100 focus:text-gray-500 transition duration-150 ease-in-out"
                    >
                      <!-- Heroicon name: x -->
                      <svg
                        class="h-6 w-6"
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M6 18L18 6M6 6l12 12"
                        />
                      </svg>
                    </button>
                  </div>
                </div>
                <div>
                  <nav class="grid gap-y-8">
                    <nuxt-link
                    v-for="option in menuOptions" :key="option.label"
                      :to="option.link"
                      class="-m-3 p-3 flex items-center space-x-3 rounded-md hover:bg-gray-50 transition ease-in-out duration-150"
                    >
                      <div class="text-lg leading-6 font-medium text-gray-900">
                        {{ option.label }}
                      </div>
                    </nuxt-link>
                  </nav>
                </div>
              </div>
              <div class="py-6 px-5 space-y-6">
                
                <div class="space-y-6">
                  <span class="w-full flex rounded-md shadow-sm" v-if="!user">
                    <nuxt-link 
                      to="/"
                      class="w-full flex items-center justify-center px-4 py-2 border border-transparent text-lg leading-6 font-medium rounded-md text-white bg-red-600 hover:bg-red-500 focus:outline-none focus:border-red-700 focus:shadow-outline-red active:bg-red-700 transition ease-in-out duration-150"
                    >
                      Registro
                    </nuxt-link>

                  </span>
                  <p v-if="user"
                    class="text-center text-lg leading-6 font-medium text-gray-500"
                  >
                    {{ user.name }}
                    <a
                      href="#"
                      class="text-red-600 hover:text-red-500 transition ease-in-out duration-150"
                    >
                      Eliminar Cuenta
                    </a>
                  </p>
                  
                </div>

              </div>
            </div>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      isOpen: false,
      menuOptions: [
        { 
          link: '/',
          label: 'Inicio'
        },
        {
          link: '#',
          label: 'Equipo'
        },
      ],
      user: []
    }
  },
  mounted() {
    this.user = JSON.parse(localStorage.getItem('user')) 
  },
  methods: {
    toggleMenu(){
      this.isOpen = !this.isOpen
    }
  }
};
</script>

<style>
</style>