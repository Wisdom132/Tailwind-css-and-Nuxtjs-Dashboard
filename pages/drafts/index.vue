<template>
  <div class="container">
    <filterdraft />
    <drafts />
  </div>
</template>

<script>
import filterdraft from '@/components/draft/filterdraft'
import drafts from '@/components/draft/index'
export default {
  components: {
    filterdraft,
    drafts
  }
}
</script>
