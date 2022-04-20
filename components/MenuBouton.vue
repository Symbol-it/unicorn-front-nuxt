<template>
    <div class="menu-bouton" @click="openOrCloseMenu">
        <img class="menu-bouton__image" src="~assets/icons/menu-hamburger.png" />
    </div>
</template>
<script>
export default{
    name: 'MenuButton',
    methods: {
        openOrCloseMenu() {
            this.$emit("openOrCloseMenu")
        }
    }
}
</script>
<style scoped>
.menu-bouton{
  width: 100px;
  height: 100px;
  position: absolute;
  right: 0;
  top: 0;
}

.menu-bouton__image{
  width: 100px;
  height: 100px;
}
</style>