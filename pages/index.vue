<template>
  <div class="unicorns">
    <unicorn-list :unicorns="unicorns" />
  </div>
</template>
<script>
import UnicornList from '@/components/UnicornList'
export default {
  name: 'IndexPage',
  components: {
    UnicornList
  },
  async asyncData ({ $http }) {
    const unicorns = await $http.$get('http://localhost:1337/unicorns?_sort=name:ASC')
    return { unicorns }
  }
}
</script>
<style scoped>
.unicorns {
  margin: 40px;
}
</style>
