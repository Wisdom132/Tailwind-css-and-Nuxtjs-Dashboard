<template>
  <section class="w-full w-1/2 px-6 py-6">
    <div class="mt-5 mb-5">
      <h3 class="text-left text-xl pl-1">All Users</h3>
    </div>
    <div class="bg-white">
      <table class="table-auto w-full border-collapse">
        <thead class="bg-gray-300">
          <tr>
            <th class="px-4  py-2">Id</th>
            <th class="px-4 py-2">Name</th>
            <th class="px-4 py-2">User Name</th>
            <th class="px-4 py-2">Email</th>
            <th class="px-4 py-2">Date Joined</th>
            <th class="px-4 py-2">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="border px-4 py-2">1</td>
            <td class="border px-4 py-2">Jammy Mill</td>
            <td class="border px-4 py-2">gentlefx</td>
            <td class="border px-4 py-2">mill@mail.com</td>
            <td class="border px-4 py-2">12/20/12</td>
            <td class="border px-4 py-2">
              <button
                class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-3 rounded"
              >
                View
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
