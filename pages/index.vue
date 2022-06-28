<template>
  <div class="unicorns">
    <unicorn-list :unicorns="unicorns" />
  </div>
</template>
<script>
import UnicornList from '@/components/UnicornList'
import FabAdd from '@/components/FabAdd.vue'
export default {
  name: 'IndexPage',
  components: {
    UnicornList,
    FabAdd
  }, 
  async asyncData ({ $http }) {
    const unicorns = await $http.$get(process.env.baseUrl + '/unicorns?_sort=name:ASC')
    return { unicorns }
  }
}
</script>
<style scoped>
.unicorns {
  margin: 40px;
}
</style>
