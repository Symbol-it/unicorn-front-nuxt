<template>
  <transition name="modal">
    <div v-show="open" class="confirmation-modal">
      <div class="confirmation-modal__content">
        <div>
          <slot />
        </div>
        <div>
          <button
            class="confirmation-modal__content__button"
            @click="cancel">
            Annuler
          </button>
          <button
            class="confirmation-modal__content__button confirmation-modal__content__button--delete"
            @click="confirmDelete">
            Supprimer
          </button>
        </div>
      </div>
    </div>
  </transition>
</template>
<script>
export default {
  name: 'DeleteModal',
  props: {
    open: Boolean,
  },
  methods: {
    cancel () {
      this.$emit('cancel')
    },
    confirmDelete () {
      this.$emit('confirm-delete')
    }
  },
  watch: {
    open () {
      if (this.open) {
        document.body.style.overflow = 'hidden';
      } else {
        document.body.style.overflow = 'initial';
      }
    }
  }
}
</script>
<style scoped>
.confirmation-modal {
  position: fixed;
  background-color: rgba(0, 0, 0, 0.5);
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.confirmation-modal__content {
  display: grid;
  row-gap: 20px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  max-width: 500px;
  width: calc(100% - 16px);
  background-color: #ffffff;
  padding: 30px;
  border-radius: 16px;
}

.confirmation-modal__content__button {
  border: none;
  background-color: transparent;
  border-radius: 8px;
  padding: 15px 20px;
  font-size: 14px;
  margin: 10px;
  cursor: pointer;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.confirmation-modal__content__button:hover {
  background-color: #e5e5e5;
}

.confirmation-modal__content__button--delete {
  background-color: #b81717;
  color: #ffffff;
}

.confirmation-modal__content__button--delete:hover {
  background-color: #ad0d0d;
}

.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.2s;
}
.modal-enter,
.modal-leave-to {
  opacity: 0;
}
</style>
