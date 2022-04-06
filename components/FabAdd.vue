<template>
    <div class="unicorns__bloc-photo" @click="addUnicorn">
      <img 
        src="~assets/icons/unicorn-horn.jpg" 
        alt="Photo d'ajout" 
        class="unicorns__bloc-photo__photo">
    </div>
</template>
<script>
export default{
    methods: {
    addUnicorn(){
      this.$router.push("create")
    }
  }
}
</script>

<style scoped>
.unicorns__bloc-photo__photo{
  width:100px;
  height: 100px;
  border-radius: 100%;  
  border: 1px solid black;
}
.unicorns__bloc-photo{
  position: fixed;
  bottom:0;
  right:0;
  cursor:pointer;
}
</style>
