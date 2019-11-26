<template>
  <div class="container">
    <filterblog />
    <blogpost />
  </div>
</template>

<script>
import filterblog from '@/components/blog/filterblog'
import blogpost from '@/components/blog/blogpost'
export default {
  components: {
    filterblog,
    blogpost
  }
}
</script>
