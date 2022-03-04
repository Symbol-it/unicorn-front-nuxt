<template>
  <div class="unicorns">
    <h1 class="unicorns__title">Unicorns</h1>
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
  font-family: 'Fredoka';
  margin: 40px;
}

.unicorns__title {
  text-align: center;
  letter-spacing: 5px;
  font-weight: bold;
}
</style>
