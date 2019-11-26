<template>
  <section class="w-full w-1/2 px-6">
    <div class="bg-white ">
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
          <tr>
            <td class="border px-4 py-2">1</td>
            <td class="border px-4 py-2">This is the title of the blog Post</td>
            <td class="border px-4 py-2">Adam</td>
            <td class="border px-4 py-2">858</td>
            <td class="border px-4 py-2">Adam</td>
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
export default {}
</script>

<style scoped></style>
