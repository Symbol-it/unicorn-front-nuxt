<template>
  <div class="app">
    <div class="app__header">
      <h1 class="app__header__title">Unicorns</h1>
      <back-button v-if="!isHomepage" />
    </div>
    <Nuxt />
  </div>
</template>
<script>
import BackButton from "../components/BackButton";
export default {
  components: {BackButton},
  computed: {
    isHomepage () {
      return this.$nuxt.$route.path === '/'
    }
  }
}
</script>
<style>
body {
  margin: 0;
}

.app {
  font-family: 'Fredoka';
}

.app__header {
  position: relative;
}

.app__header__title {
  margin: 0;
  padding: 30px 0;
  text-align: center;
  letter-spacing: 5px;
  font-weight: bold;
}

.app__header__title:hover {
  cursor: pointer;
}
</style>
