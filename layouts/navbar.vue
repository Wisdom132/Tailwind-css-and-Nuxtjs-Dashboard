<template>
  <header
    class="fixed color z-50 h-16 w-full  shadow flex items-center justify-between"
  >
    <div class="flex items-center h-full ">
      <div
        class="flex items-center text-center h-full w-48 border-r bg-midnightblue-500 border-grey-dark"
      >
        <span class="w-full text-white text-sm uppercase font-extrabold "
          >WEBARTISAN.BE</span
        >
      </div>
      <div class="flex items-center w-64">
        <form action="" class="w-full h-full px-3 flex items-center">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            width="24"
            height="24"
            class="h-6 w-6 text-dark fill-current"
          >
            <path
              class="heroicon-ui"
              d="M16.32 14.9l5.39 5.4a1 1 0 0 1-1.42 1.4l-5.38-5.38a8 8 0 1 1 1.41-1.41zM10 16a6 6 0 1 0 0-12 6 6 0 0 0 0 12z"
            />
          </svg>
          <input
            type="search"
            class="appearance-none bg-grey-darker h-full w-full py-2 px-2 text-dark hover:bg-gray-300 focus:border-gray-700"
            placeholder="Search..."
          />
        </form>
      </div>
    </div>
    <button
      @click="isOpen = !isOpen"
      class="relative z-10 block h-8 mr-6  overflow-hidden  text-white focus:outline-none focus:border-white"
    >
      Account
    </button>
    <button
      v-if="isOpen"
      @click="isOpen = false"
      tabindex="-1"
      class="fixed inset-0 h-full w-full bg-black opacity-50 cursor-default"
    ></button>
    <div
      v-if="isOpen"
      class="absolute right-0 mt-2 py-2 w-48 bg-white rounded-lg shadow-xl"
    >
      <a href="#" class="block px-4 py-2 text-gray-800" @click="signOut"
        >Sign out</a
      >
    </div>
  </header>
</template>
<script>
import auth from '../utils/auth'

export default {
  data() {
    return {
      isOpen: false
    }
  },
  methods: {
    signOut() {
      localStorage.removeItem('token')
      localStorage.removeItem('currentUser')
      auth.logoutUser()
      this.$router.push('/')
    },
    error(message) {
      swal('Error', message, 'error')
    }
  }
}
</script>
<style scoped>
.w-48 {
  width: 15rem !important;
}

.color {
  background: #14233b;
}
</style>
