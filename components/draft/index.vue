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
          <tr v-for="(post, index) in drafts" :key="index">
            <td class="border px-4 py-2">{{ parseInt(index + 1) }}</td>
            <td class="border px-4 py-2">{{ post.title }}</td>
            <td class="border px-4 py-2">{{ post.dateCreated | moment }}</td>
            <td class="border px-4 py-2">
              <span v-for="(data, index) in post.tags" :key="index">
                {{
                data
                }}
              </span>
            </td>
            <td class="border px-4 py-2">{{ post.category.title }}</td>
            <td class="border px-4 py-2">
              <button
                @click="deleteDraft(post._id)"
                class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-2 rounded"
              >Delete</button>

              <router-link
                :to="'/drafts/'+post._id"
                class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-2 rounded"
              >View</router-link>

              <button
                @click="toggleModal"
                class="modal-open bg-teal-500 hover:bg-teal-700 text-white font-bold py-2 px-2 rounded"
              >Edit</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <editdraft />
  </section>
</template>

<script>
import editdraft from './editdraft'
import loader from '@/components/loader/loader'
import moment from 'moment'
export default {
  components: {
    loader,
    editdraft
  },
  filters: {
    moment: function(date) {
      return moment(date).format('MMMM Do YYYY')
    }
  },
  data() {
    return {
      loading: false,
      drafts: [],
      time: 0,
      duration: 5000
    }
  },
  methods: {
    async getAllDrafts() {
      this.loading = true
      try {
        let response = await this.$axios.get('draft')
        this.drafts = response.data.data
        this.loading = false
        console.log(this.drafts)
      } catch (err) {
        this.loading = false
        console.log(err)
      }
    },
    toggleModal() {
      const body = document.querySelector('body')
      const modal = document.querySelector('.modal')
      modal.classList.toggle('opacity-0')
      modal.classList.toggle('pointer-events-none')
      body.classList.toggle('modal-active')
    },

    deleteDraft(id) {
      swal({
        title: 'Are you sure?',
        text:
          'Once deleted, you will not be able to recover this imaginary file!',
        icon: 'warning',
        buttons: true,
        dangerMode: true
      }).then((willDelete) => {
        if (willDelete) {
          this.$axios
            .delete(`blog/${id}`)
            .then((response) => {
              swal('Post Has been Deleted!', {
                icon: 'success'
              })
              this.getBlogPost()
            })
            .catch((err) => {
              console.log(err)
              swal('Error', 'Something Went Wrong', 'error')
            })
        } else {
          swal('Your imaginary file is safe!')
        }
      })
    }
  },
  created() {
    this.getAllDrafts()
  }
}
</script>


