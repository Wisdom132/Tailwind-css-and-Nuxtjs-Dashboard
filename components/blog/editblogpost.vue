<template>
  <!-- modal  -->
  <div
    class="modal opacity-0 pointer-events-none absolute z-50 w-full top-0 mt-10 left-0 flex items-center justify-center"
  >
    <div class="modal-overlay absolute w-full bg-gray-900 opacity-50"></div>

    <div
      class="modal-container bg-white w-11/12 md:max-w-3xl mx-auto rounded shadow-lg z-50 overflow-y-auto"
    >
      <div
        @click="closeModal"
        class="modal-close absolute top-0 right-0 cursor-pointer flex flex-col items-center mt-4 mr-4 text-white text-sm z-50"
      >
        <svg
          class="fill-current text-white"
          xmlns="http://www.w3.org/2000/svg"
          width="18"
          height="18"
          viewBox="0 0 18 18"
        >
          <path
            d="M14.53 4.53l-1.06-1.06L9 7.94 4.53 3.47 3.47 4.53 7.94 9l-4.47 4.47 1.06 1.06L9 10.06l4.47 4.47 1.06-1.06L10.06 9z"
          />
        </svg>
      </div>

      <!-- Add margin if you want to see some of the overlay behind the modal-->
      <div class="modal-content py-4 text-left px-6">
        <!--Title-->
        <div class="flex justify-between items-center pb-3">
          <p class="text-2xl font-bold">Edit Post</p>
          <div class="modal-close cursor-pointer z-50" @click="closeModal">
            <svg
              class="fill-current text-black"
              xmlns="http://www.w3.org/2000/svg"
              width="18"
              height="18"
              viewBox="0 0 18 18"
            >
              <path
                d="M14.53 4.53l-1.06-1.06L9 7.94 4.53 3.47 3.47 4.53 7.94 9l-4.47 4.47 1.06 1.06L9 10.06l4.47 4.47 1.06-1.06L10.06 9z"
              />
            </svg>
          </div>
        </div>
        <!--Body-->
        <form class="w-full bg-white px-2 pt-10" @submit.prevent="updatePost(editableblog._id)">
          <h1 class="text-left text-xl mb-6">Edit Post</h1>

          <div class="flex flex-wrap -mx-3 mb-6">
            <div class="w-full lg:w-3/4 sm:w-full px-3 mb-6 md:mb-0">
              <label
                class="block uppercase text-left tracking-wide text-gray-700 text-xs font-bold mb-2"
                for="grid-first-name"
              >Post Title</label>
              <input
                v-model="editableblog.title"
                class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-500 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
                id="grid-first-name"
                type="text"
                placeholder="Jane"
              />
            </div>

            <div class="w-full lg:w-1/4 sm:w-full px-3 mb-6 md:mb-0">
              <label
                class="block uppercase text-left tracking-wide text-gray-700 text-xs font-bold mb-2"
                for="grid-first-name"
              >Upload Image</label>
              <input
                class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-500 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
                id="grid-first-name"
                type="file"
                ref="file"
                placeholder="Jane"
              />
            </div>
          </div>
          <div class="flex flex-wrap -mx-3 mb-6">
            <div class="w-full lg:w-1/2 sm:w-full px-3 mb-6 md:mb-0">
              <label
                class="block uppercase text-left tracking-wide text-gray-700 text-xs font-bold mb-2"
                for="grid-first-name"
              >Tags</label>
              <input
                v-model="editableblog.tags"
                class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-500 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
                id="grid-first-name"
                type="text"
                placeholder="Jane"
              />
            </div>
            <div class="w-full lg:w-1/2 sm:w-full l px-3 mb-6 md:mb-0">
              <label
                class="block uppercase text-left tracking-wide text-gray-700 text-xs font-bold mb-2"
                for="grid-first-name"
              >Category</label>
              <select
                v-model="editableblog.category"
                class="form-select appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-500 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
                id="grid-state"
              >
                <option :value="null">Select an option</option>
                <option
                  v-for="(category, index) in categories"
                  :key="index"
                  :value="category._id"
                >{{ category.title }}</option>
              </select>
            </div>
          </div>
          <div class="flex flex-wrap -mx-3 mb-6">
            <div class="w-full px-3 mb-6 md:mb-0">
              <label
                class="block uppercase text-left tracking-wide text-gray-700 text-xs font-bold mb-2"
                for="grid-first-name"
              >Content</label>
              <ckeditor
                v-model="editableblog.content"
                :editor="editor"
                id="editor"
                :config="editorConfig"
              ></ckeditor>
            </div>
            <div class="flex flex-wrap -mx-3 mb-6 mt-5 ml-1">
              <div class="w-full px-3 mb-6 md:mb-0">
                <div v-if="loading">
                  <loader />
                </div>
                <button
                  class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                  type="submit"
                >Edit Post</button>
              </div>
            </div>
          </div>
        </form>

        <!--Footer-->
        <div class="flex justify-end pt-2">
          <button
            @click="closeModal"
            class="modal-close px-4 bg-indigo-500 p-3 rounded-lg text-white hover:bg-indigo-400"
          >Close</button>
        </div>
      </div>
    </div>
  </div>
  <!-- modal  -->
</template>
<script>
let ClassicEditor
if (process.client) {
  ClassicEditor = require('@ckeditor/ckeditor5-build-classic')
}
import swal from 'sweetalert'
import loader from '@/components/loader/loader'

export default {
  data() {
    return {
      categories: [],
      editor: ClassicEditor,
      editorConfig: {},
      loading: false
    }
  },
  props: ['editableblog'],
  components: {
    loader
  },
  methods: {
    closeModal() {
      this.toggleModal()
    },
    async getAllCategories() {
      try {
        let response = await this.$axios.get('category')
        this.categories = response.data.data
      } catch (err) {
        console.log(err)
      }
    },

    async updatePost(id) {
      this.loading = true
      try {
        let response = await this.$axios.put(
          `blog/update/${id}`,
          this.editableblog
        )
        swal('Success', 'Post Updated', 'success')
        this.loading = false
        this.closeModal()
      } catch (err) {
        this.loading = false
        swal('Error', 'Something Went Wrong', 'error')
      }
    },

    toggleModal() {
      const body = document.querySelector('body')
      const modal = document.querySelector('.modal')
      modal.classList.toggle('opacity-0')
      modal.classList.toggle('pointer-events-none')
      body.classList.toggle('modal-active')
    }
  },
  mounted() {
    this.getAllCategories()
  }
}
</script>
<style>
.modal {
  transition: opacity 0.25s ease;
}
body.modal-active {
  overflow-x: hidden;
  overflow-y: visible !important;
}
</style>
