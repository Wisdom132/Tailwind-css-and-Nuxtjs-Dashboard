<template>
  <section class=" p-6">
    <form class="w-full container bg-white border rounded shadow p-5 mr-4">
      <div class="flex flex-wrap -mx-3 mb-3">
        <div class="w-full md:w-1/4 px-3 mb-6 md:mb-0">
          <label
            class="block uppercase tracking-wide text-left text-gray-700 text-xs font-bold mb-2"
            for="grid-first-name"
          >
            Title
          </label>
          <input
            class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
            id="grid-first-name"
            type="text"
            placeholder="Facebook Hacked"
          />
        </div>
        <div class="w-full md:w-1/4 px-3">
          <label
            class="block uppercase text-left tracking-wide text-gray-700 text-xs font-bold mb-2"
            for="grid-last-name"
          >
            Date
          </label>
          <input
            class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
            id="grid-last-name"
            type="text"
            placeholder="Doe"
          />
        </div>
        <div class="w-full md:w-1/4 px-3">
          <label
            class="block uppercase text-left tracking-wide text-gray-700 text-xs font-bold mb-2"
            for="grid-last-name"
          >
            Category
          </label>
          <select
            class="block appearance-none w-full bg-gray-200 border border-gray-200 hover:border-gray-500 py-3 px-4 rounded shadow leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
          >
            <option>Option 2</option>
            <option>Option 3</option>
          </select>
        </div>
        <div class="w-full md:w-1/4 px-3 ">
          <button
            class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 mt-6 rounded"
          >
            Reset Filter
          </button>
          <button
            class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 mt-6 rounded"
          >
            Search
          </button>
        </div>
      </div>
    </form>
  </section>
</template>

<script>
export default {}
</script>
<style scoped></style>
