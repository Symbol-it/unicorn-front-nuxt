<template>
  <div class="unicorns">
    <div class="unicorns__bloc-photo" @click="addUnicorn">
      <img src="~assets/icons/unicorn-horn.jpg" alt="Photo d'ajout" class="unicorns__bloc-photo__photo">
    </div>
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
    const unicorns = await $http.$get('http://localhost:1337/unicorns?_sort=name:ASC');
    return { unicorns };
  },

  methods: {
    addUnicorn(){
      this.$router.push("addUnicorn");
    }
  }
}
</script>
<style scoped>
.unicorns {
  margin: 40px;
}
.unicorns__bloc-photo__photo{
  width:100px;
  height: 100px;
  border-radius: 100%;  
  border: 1px solid black;
}
.unicorns__bloc-photo{
  position: fixed;
  bottom:0%;
  right:1%;
  cursor:pointer;
}
</style>
