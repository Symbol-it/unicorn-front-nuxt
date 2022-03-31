<template>
  <div class="container">
    <h1 v-if="error.statusCode === 404" class="error--text-align">Es-tu perdu ?</h1>
    <h1 v-else-if="error.statusCode === 500" class="error--text-align"> {{ error.message }} </h1>
    <h1 v-else class="error--text-align">Une erreur s'est produite</h1>
    <nuxt-link to="/" class="container__nuxt-link error--text-align"> &gt; Accueil &lt; </nuxt-link>
  </div>
</template>
<script>
export default {
  props: ['error']
}
</script>
<style scoped>
.container{
  margin:auto;
  max-width: 1200px;
  width: 100%;
}

.error--text-align{
  text-align: center;
}

.container__nuxt-link{
  font-size: 24px;
  text-decoration: none;
  display: block;
}

.container__nuxt-link:visited{
  color: rgb(131, 197, 255);
}
</style>