<template>
  <div>
    <div class="xl:py-10 sidebar-layout">
      <div class="group relative sidebar-item with-children">
        <nuxt-link
          to="/dashboard"
          class="block xl:flex xl:items-center text-center xl:text-left shadow-light xl:shadow-none py-6 xl:py-2 xl:px-4 border-l-4 border-transparent hover:bg-gray-800"
        >
          <i class="mdi mdi-view-dashboard text-white px-2"></i>

          <div class="text-white text-base">Dashboard</div>
        </nuxt-link>
      </div>
      <div class="group relative sidebar-item with-children">
        <nuxt-link
          to="/addpost"
          class="block xl:flex xl:items-center text-center xl:text-left shadow-light xl:shadow-none py-6 xl:py-2 xl:px-4 border-l-4 border-transparent hover:bg-gray-800"
        >
          <i class="mdi mdi-pen text-white px-2"></i>

          <div class="text-white text-base">Add Post</div>
        </nuxt-link>
      </div>
      <div class="group relative sidebar-item with-children mt-2">
        <nuxt-link
          to="/blog"
          class="block xl:flex xl:items-center text-center xl:text-left shadow-light xl:shadow-none py-6 xl:py-2 xl:px-4 border-l-4 border-transparent hover:bg-gray-800"
        >
          <i class="mdi mdi-format-align-justify text-white px-2"></i>
          <div class="text-white text-base">Blog Posts</div>
        </nuxt-link>
      </div>
      <div class="group relative sidebar-item with-children mt-2">
        <nuxt-link
          to="/category"
          class="block xl:flex xl:items-center text-center xl:text-left shadow-light xl:shadow-none py-6 xl:py-2 xl:px-4 border-l-4 border-transparent hover:bg-gray-800"
        >
          <i class="mdi mdi-plus text-white px-2"></i>
          <div class="text-white text-base">Category</div>
        </nuxt-link>
      </div>

      <div class="group relative sidebar-item with-children mt-2">
        <nuxt-link
          to="/users"
          class="block xl:flex xl:items-center text-center xl:text-left shadow-light xl:shadow-none py-6 xl:py-2 xl:px-4 border-l-4 border-transparent hover:bg-gray-800"
        >
          <i class="mdi mdi-account mdi-38px text-white px-2"></i>
          <div class="text-white text-base">Users</div>
        </nuxt-link>
      </div>
      <div class="group relative sidebar-item with-children mt-2">
        <nuxt-link
          to="/drafts"
          class="block xl:flex xl:items-center text-center xl:text-left shadow-light xl:shadow-none py-6 xl:py-2 xl:px-4 border-l-4 border-transparent hover:bg-gray-800"
        >
          <i class="mdi mdi-account mdi-38px text-white px-2"></i>
          <div class="text-white text-base">Drafts</div>
        </nuxt-link>
      </div>
      <div class="group relative sidebar-item with-children mt-2">
        <a
          @click="signOut"
          class="block xl:flex xl:items-center text-center xl:text-left shadow-light xl:shadow-none py-6 xl:py-2 xl:px-4 border-l-4 border-transparent hover:bg-gray-800"
        >
          <i class="mdi mdi-logout mdi-38px text-white px-2"></i>
          <div class="text-white text-base">Logout</div>
        </a>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {}
  },
  methods: {
    signOut() {
      localStorage.removeItem('token')
      localStorage.removeItem('currentUser')
      auth.logoutUser()
      this.$router.push('/')
    },
    error(message) {
      swal('Sorry', message, 'error')
    }
  }
}
</script>
<style scoped>
.sidebar-layout {
  position: fixed;
  overflow-y: auto;
}
@media (max-width: 375px) {
  .sidebar-layout {
    position: fixed;
    overflow-y: auto;
  }
}
@media (max-width: 639px) {
  .sidebar-layout {
    position: fixed;
    overflow-y: auto;
  }
}
@media (max-width: 768px) {
  .sidebar-layout {
    position: fixed;
    overflow-y: auto;
  }
}
</style>
