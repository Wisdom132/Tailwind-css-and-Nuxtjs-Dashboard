<template>
  <section>
    <div class="px-6 py-10">
      <div class="flex flex-wrap -mx-2">
        <div class="w-full sm:w-1/2 md:w-1/2 lg:w-1/3 xl:1/3 mb-5  px-2">
          <div class="bg-gray-400 h-100%">
            <div class="bg-white">
              <div
                class="font-bold text-xl mb-2 border border-gray-300 bg-gray-100 py-2"
              >
                Add Custome Category
              </div>
              <form class="bg-white shadow-md rounded px-3 pt-6 pb-8 mb-4">
                <div class="mb-4">
                  <label
                    class="block text-gray-700 text-sm text-left font-bold mb-2"
                    for="username"
                  >
                    Title
                  </label>
                  <input
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                    id="username"
                    type="text"
                    placeholder="Title"
                  />
                </div>

                <div class="mb-4">
                  <label
                    class="block text-gray-700 text-sm text-left font-bold mb-2"
                    for="username"
                  >
                    Description
                  </label>
                  <textarea
                    class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                    placeholder="Your Category Description"
                    rows="6"
                  ></textarea>
                </div>

                <div class="flex items-center justify-between">
                  <button
                    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                    type="button"
                  >
                    Add
                  </button>
                </div>
              </form>
            </div>
          </div>
        </div>
        <div class="w-full sm:w-1/2 md:w-1/2 lg:w-2/3 xl:w-2/3 mb-5  px-2">
          <div class="bg-gray-400 h-100%">
            <div class="bg-white ">
              <table class="table-fixed w-full border-collapse">
                <thead class="bg-gray-300">
                  <tr>
                    <th class="px-4 py-2">Index</th>
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
                    <td class="border px-4 py-2">
                      This is the title of the blog Post
                    </td>
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
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {}
</script>

<style scoped></style>
