<template>
  <section class="w-full w-1/2 px-6">
    <div v-if="loading">
      <loader />
    </div>
    <div class="bg-white" v-else>
      <div class="container text-left p-10" v-if="preview">
        <div class="bg-gray-300">
          <img
            class="object-cover cover-photo h-64 w-full p-5"
            :src="preview.featured_image[0]"
            alt
          />
        </div>
        <h1 class="text-left text-3xl my-8">{{preview.title}}</h1>
        <h6>
          <span class="text-lg">Category</span>
          {{preview.category.title}}
        </h6>
        <h6 class="mb-5">
          <span class="text-lg">User</span>
          {{preview.drafter.name}}
        </h6>
        <h6 class="mb-5">
          <span class="text-lg">User Phone</span>
          {{preview.drafter.phone}}
        </h6>
        <h6 class="mb-5">
          <div v-if="preview.isCompleted">
            <span class="text-lg">status</span>
            In-Progress
          </div>
          <div v-else>
            <span class="text-lg">status</span>
            Completed
          </div>
        </h6>
        <h6 class="mb-5">
          <span class="text-lg">Date Created</span>
          {{preview.dateCreated |moment}}
        </h6>
        <p v-html="preview.content" class="content text-justify text-gray-800"></p>
      </div>
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
      preview: null,
      loading: true
    }
  },

  methods: {
    async getDraftDetails(id) {
      this.loading = true
      try {
        let response = await this.$axios.$get(`draft/${id}`)
        this.preview = response.response
        this.loading = false
      } catch (err) {
        this.loading = false
        console.log(err)
      }
    }
  },
  created() {
    this.getDraftDetails(this.$route.params.id)
  }
}
</script>
<style scoped>
.content {
  line-height: 2.25rem;
}
</style>