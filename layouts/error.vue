<template>
  <div class="container">
    <h1 v-if="error.statusCode === 404">Are you lost ?</h1>
    <h1 v-else-if="error.statusCode === 500"> Error server </h1>
    <h1 v-else>An error occurred</h1>
    <nuxt-link to="/" class="container__nuxt-link"> &gt; Homepage &lt; </nuxt-link>
  </div>
</template>
<script>
export default {
  props: ['error'],
  layout: 'blog' // you can set a custom layout for the error page
}
</script>
<style scoped>
.container{
  text-align: center;
}

.container__nuxt-link{
  font-size: 24px;
  text-decoration: none;
}

.container__nuxt-link:visited{
  color: rgb(131, 197, 255);
}
</style>