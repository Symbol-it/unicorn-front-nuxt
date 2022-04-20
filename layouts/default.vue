<template>
  <div class="app">
    <div :class="['app_header', {'app__header__open' : this.menuOpen}]">
      <h1 class="app__header__title">Unicorns</h1>
      <back-button v-if="!isHomepage" @close-menu="closeMenu"/>
      <menu-bouton @openOrCloseMenu="openOrCloseMenu"/>
      <div class="app__header__menu-title" v-if="menuOpen">
       <item-menu v-for="(items,index) in itemsMenu" :item="items" :key="index" @redirection="goToMenuItem"/>
      </div>
    </div>
    <Nuxt />

    <fab-add v-if="isHomepage" @close-menu="closeMenu"/>
  </div>
</template>
<script>
import BackButton from "@/components/BackButton";
import MenuBouton from '@/components/MenuBouton.vue';
import ItemMenu from '@/components/ItemMenu.vue';
import FabAdd from '@/components/FabAdd.vue';
export default {
  components: {BackButton, MenuBouton, ItemMenu, FabAdd},

  async fetch(){
    this.itemsMenu = await this.$http.$get(process.env.baseUrl + '/navigations?_sort=ordre').then(array => { return array })
  },

  data() {
    return {
      menuOpen : false,
      itemsMenu : []
    }
  },
  computed: {
    isHomepage () {
      return this.$nuxt.$route.path === '/'
    }
  },

  methods: {
    openOrCloseMenu(){
      this.menuOpen = !this.menuOpen
    },

    goToMenuItem(url){
      this.$router.push(url)
      this.menuOpen = false
    },

    closeMenu(){
      this.menuOpen = false
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

.app__header__open{
  background-color: rgba(138,43,226,0.5);
}
</style>
