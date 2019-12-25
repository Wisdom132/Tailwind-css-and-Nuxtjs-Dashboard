<template>
  <section class="w-full w-1/2 px-6 py-6">
    <div class="bg-white p-4">
      <div class="mt-5 mb-5">
        <h3 class="text-left text-xl pl-1">All Users</h3>
      </div>
      <div v-if="loading">
        <loader />
      </div>
      <div class="bg-white" v-else>
        <table class="table-auto w-full border-collapse">
          <thead class="bg-gray-300">
            <tr>
              <th class="px-4 py-2">Id</th>

              <th class="px-4 py-2">User Name</th>
              <th class="px-4 py-2">Email</th>
              <th class="px-4 py-2">Date Joined</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(user, index) in users" :key="index">
              <td class="border px-4 py-2">{{ parseInt(index + 1) }}</td>

              <td class="border px-4 py-2">{{ user.username }}</td>
              <td class="border px-4 py-2">{{ user.email }}</td>
              <td class="border px-4 py-2">{{ user.dateCreated | moment }}</td>
            </tr>
          </tbody>
        </table>
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
  data() {
    return {
      users: [],
      loading: false
    }
  },
  filters: {
    moment: function(date) {
      return moment(date).format('MMMM Do YYYY')
    }
  },
  methods: {
    async getAllUsers() {
      this.loading = true
      try {
        let response = await this.$axios.get('users/users')
        this.users = response.data
        this.loading = false
      } catch (err) {
        this.loading = false
        console.log(err)
      }
    }
  },

  created() {
    this.getAllUsers()
  }
}
</script>

<style scoped></style>
