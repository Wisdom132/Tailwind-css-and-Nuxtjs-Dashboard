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
    <div class="flex items-center h-full text-sm">
      <div class="flex items-center h-full">
        <a href="#" class="flex items-center text-white h-full px-4">Support</a>
        <div class="group relative h-full">
          <a
            href="#"
            class="text-white flex items-center h-full bg-grey-darkest px-4"
          >
            Account
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
              width="24"
              height="24"
              class="h-6 w-6 text-grey-darker fill-current ml-1"
            >
              <path
                class="heroicon-ui"
                d="M15.3 9.3a1 1 0 0 1 1.4 1.4l-4 4a1 1 0 0 1-1.4 0l-4-4a1 1 0 0 1 1.4-1.4l3.3 3.29 3.3-3.3z"
              />
            </svg>
          </a>
          <div
            class="hidden group-hover:block absolute pin-r top-full w-48 bg-black"
          >
            <a
              href="#"
              class="block text-left py-3 px-3 text-white hover:text-blue-dark text-xs"
            >
              My Account
            </a>
            <a
              href="#"
              class="block text-left py-3 px-3 text-white hover:text-blue-dark text-xs"
            >
              Edit Account
            </a>
            <a
              href="#"
              class="block text-left py-3 px-3 text-white hover:text-blue-dark text-xs"
            >
              Logout
            </a>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>
<script>
export default {}
</script>
<style scoped>
.w-48 {
  width: 15rem !important;
}

.color {
  background: #14233b;
}
</style>
