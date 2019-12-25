<template>
  <section class="w-full w-1/2 px-6">
    <div v-if="loading">
      <loader />
    </div>
    <div class="bg-white" v-else>
      <table class="table-auto w-full border-collapse">
        <thead class="bg-gray-300">
          <tr>
            <th class="px-4 py-2">Id</th>
            <th class="px-4 py-2">Title</th>
            <th class="px-4 py-2">Date Posted</th>
            <th class="px-4 py-2">Tags</th>
            <th class="px-4 py-2">Category</th>
            <th class="px-4 py-2">Action</th>
          </tr>
        </thead>

        <tbody>
          <tr v-for="(post, index) in posts" :key="index">
            <td class="border px-4 py-2">{{ parseInt(index + 1) }}</td>
            <td class="border px-4 py-2">{{ post.title }}</td>
            <td class="border px-4 py-2">{{ post.dateCreated | moment }}</td>
            <td class="border px-4 py-2">
              <span v-for="(data, index) in post.tags" :key="index">
                {{ data }}
              </span>
            </td>
            <td class="border px-4 py-2">{{ post.category.title }}</td>
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
  </section>
</template>

<script>
import loader from '@/components/loader/loader'
import moment from 'moment'
export default {
  components: {
    loader
  },
   filters: {
    moment: function(date) {
      return moment(date).format('MMMM Do YYYY')
    }
  },
  data() {
    return {
      loading: false,
      posts: []
    }
  },
  methods: {
    async getBlogPost() {
      this.loading = true
      try {
        let response = await this.$axios.get('blog')
        this.posts = response.data.data
        this.loading = false
        console.log(this.posts)
      } catch (err) {
        this.loading = false
        console.log(err)
      }
    }
  },
  created() {
    this.getBlogPost()
  }
}
</script>

<style scoped></style>
