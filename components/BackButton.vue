<template>
  <button class="back-button" @click="goBack">
    <img
      class="back-button__icon"
      src="~assets/icons/arrow-left.svg"
      alt="Icône flèche">
    <div class="app__header__button__text">Retour</div>
  </button>
</template>
<script>
export default {
  name: 'BackButton',
  methods: {
    goBack () {
      this.$router.go(-1)
    }
  },
}
</script>
<style scoped>
.back-button {
  font-size: 14px;
  letter-spacing: 2px;
  text-transform: uppercase;
  display: flex;
  gap: 10px;
  border: none;
  background-color: transparent;
  cursor: pointer;
  align-items: center;
  position: absolute;
  top: 50%;
  left: 0;
  transform: translateY(-50%);
  padding: 20px;
}

.back-button__icon {
  height: 30px;
}
</style>
