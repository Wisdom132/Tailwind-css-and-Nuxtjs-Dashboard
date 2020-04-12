<template>
  <section class="mx-10 pt-10">
    <form class="w-full bg-white px-32 pt-10" @submit.prevent="addNewBlogPost">
      <h1 class="text-left text-xl mb-6">Add Blog Post</h1>

      <div class="flex flex-wrap -mx-3 mb-6">
        <div class="w-full lg:w-3/4 sm:w-full px-3 mb-6 md:mb-0">
          <label
            class="block uppercase text-left tracking-wide text-gray-700 text-xs font-bold mb-2"
            for="grid-first-name"
          >Post Title</label>
          <input
            class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-500 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
            id="grid-first-name"
            type="text"
            v-model="data.title"
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
            @change="handleFileUpload()"
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
            class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-500 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
            id="grid-first-name"
            type="text"
            v-model="data.tags"
            placeholder="Jane"
          />
        </div>
        <div class="w-full lg:w-1/2 sm:w-full l px-3 mb-6 md:mb-0">
          <label
            class="block uppercase text-left tracking-wide text-gray-700 text-xs font-bold mb-2"
            for="grid-first-name"
          >Category</label>
          <select
            v-model="data.category"
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
          <ckeditor :editor="editor" id="editor" v-model="data.content" :config="editorConfig"></ckeditor>
        </div>
        <div class="flex flex-wrap -mx-3 mb-6 mt-5 ml-1">
          <div class="w-full px-3 mb-6 md:mb-0">
            <button
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              type="submit"
            >Add Post</button>
          </div>
        </div>
      </div>
    </form>
  </section>
</template>
<script>
let ClassicEditor
if (process.client) {
  ClassicEditor = require('@ckeditor/ckeditor5-build-classic')
}
import swal from 'sweetalert'
export default {
  data() {
    return {
      categories: [],
      data: {
        title: '',
        tags: [],
        category: '',
        featured_image: '',
        content: ''
      },
      editor: ClassicEditor,
      editorConfig: {}
    }
  },
  methods: {
    handleFileUpload() {
      this.data.featured_image = this.$refs.file.files[0]
      console.log(this.data.featured_image)
    },
    async getAllCategories() {
      try {
        let response = await this.$axios.get('category')
        this.categories = response.data.data
      } catch (err) {
        console.log(err)
      }
    },
    async addNewBlogPost() {
      try {
        let formData = new FormData()
        formData.append('featured_image', this.data.featured_image)
        formData.append('title', this.data.title)
        formData.append('category', this.data.category)
        formData.append('content', this.data.content)
        formData.append('tags', this.data.tags)
        let response = await this.$axios.post('blog', formData)
        console.log(response)

        swal('Success', 'Post Published', 'success')

        this.data = {}
      } catch (err) {
        swal('Error', 'Something Went Wrong', 'error')
        console.log(err)
      }
    }
  },
  created() {
    this.getAllCategories()
  }
}
</script>
<style>
.ck-editor__editable_inline {
  min-height: 300px;
}
</style>
