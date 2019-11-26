<template>
  <div>
    <div class="wrapper">
      <nav-bar />

      <div id="main">
        <div class="bg-midnightblue-500 relative pt-16 h-full min-h-screen">
          <div class="xl:py-5 ">
            <side-bar />
          </div>
        </div>
        <div class="h-full pt-16">
          <div class="text-center bg-gray-200 h-full w-full text-grey-darkest">
            <nuxt />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import navbar from '@/layouts/navbar'
import sidebar from '@/layouts/sidebar'
export default {
  components: {
    'nav-bar': navbar,
    'side-bar': sidebar
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Muli&display=swap');
* {
  font-family: 'Muli', sans-serif;
}
#main {
  display: grid;
  grid-template-columns: 6rem auto;
  /* Or grid-template-columns: config('width.24') auto; */
}

@media (min-width: 1200px) {
  /* Or @media (min-width: config('screens.xl')) { */

  #main {
    grid-template-columns: 15rem auto;
  }
  /* Or #main { grid-template-columns: config('width.48') auto; } */
}

a {
  text-decoration: none;
  /* Or @apply .no-underline; */
}

/* Just a new padding size */
.pt-16 {
  padding-top: 4rem;
}

/*
 * Just some customized new utilities needed for the submenus
 * Add this before
 */
.top-full {
  top: 100%;
}
.left-full {
  left: 100%;
}

/*
 * This hacks is just needed in Codepen because the previous rules are prioritary to xl:pin-none.
 * In your own config this should not be needed.
 */

@media (min-width: 1200px) {
  .xl:pin-none {
    left: auto;
  }
}

/* 
 * Active "group-hover" for the "display" module in your
 * tailwind.js config file like this:
 * 
 * display: ['responsive', 'group-hover']
 *
 * More info on https://tailwindcss.com/docs/state-variants/#group-hover
 */
.group:hover .group-hover\:block {
  display: block;
}
.bg-midnightblue-500 {
  background: #14233b;
}
</style>
