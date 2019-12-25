<template>
  <section>
    <div class="px-6 py-10">
      <div class="flex flex-wrap -mx-2">
        <div class="w-full sm:w-1/2 md:w-1/2 lg:w-1/3 xl:1/3 mb-5 px-2">
          <div class="bg-gray-400 h-100%">
            <div class="bg-white">
              <div
                class="font-bold text-xl mb-2 border border-gray-300 bg-gray-100 py-2"
              >
                Add Custome Category
              </div>
              <form
                class="bg-white shadow-md rounded px-3 pt-6 pb-8 mb-4"
                @submit.prevent="addNewCategory"
              >
                <div class="mb-4">
                  <label
                    class="block text-gray-700 text-sm text-left font-bold mb-2"
                    for="username"
                    >Title</label
                  >
                  <input
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                    id="username"
                    type="text"
                    v-model="category.title"
                    placeholder="Title"
                  />
                </div>

                <div class="mb-4">
                  <label
                    class="block text-gray-700 text-sm text-left font-bold mb-2"
                    for="username"
                    >Description</label
                  >
                  <textarea
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                    placeholder="Your Category Description"
                    rows="6"
                    v-model="category.description"
                  ></textarea>
                </div>

                <div class="flex items-center justify-between">
                  <button
                    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                    type="submit"
                  >
                    Add
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
        <div class="w-full sm:w-1/2 md:w-1/2 lg:w-2/3 xl:w-2/3 mb-5 px-2">
          <div class="bg-gray-400 h-100%">
            <div v-if="loading">
              <loader />
            </div>
            <div class="bg-white" v-else>
              <table class="table-auto w-full border-collapse">
                <thead class="bg-gray-300">
                  <tr>
                    <th class="px-4 py-2">Index</th>
                    <th class="px-4 py-2">Title</th>
                    <th class="px-4 py-2">Description</th>

                    <th class="px-4 py-2">Date Created</th>
                    <th class="px-4 py-2">Action</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(category, index) in categories" :key="index">
                    <td class="border px-4 py-2">{{ parseInt(index + 1) }}</td>
                    <td class="border px-4 py-2">
                      {{ category.title }}
                    </td>
                    <td class="border px-4 py-2">{{ category.description }}</td>
                    <td class="border px-4 py-2">{{ category.dateCreated | moment }}</td>

                    <td class="border px-4 py-2">
                      <button
                        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-2 rounded"
                      >
                        Delete
                      </button>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import loader from '@/components/loader/loader'
import moment from 'moment'
export default {
  components:{
    loader
  },
   filters: {
    moment: function(date) {
      return moment(date).format('MMMM Do YYYY')
    }
  },
  data() {
    return {
      loading:false,
      categories: [],
      category: {
        title: '',
        description: ''
      }
    }
  },
  methods: {
    async getAllCategories() {
      this.loading = true
      try {
        let response = await this.$axios.get('category')
        this.categories = response.data.data
        this.loading = false
      } catch (err) {
        console.log(err)
        this.loading = false
      }
    },
    async addNewCategory() {
      try {
        let response = await this.$axios.post('category', this.category)
        console.log(response)
        this.getAllCategories()
        this.category = {}
      } catch (err) {
        console.log(err)
      }
    }
  },
  created() {
    this.getAllCategories()
  }
}
</script>

<style scoped></style>
