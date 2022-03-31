<template>
    <div class="unicorn-card">
        <div class="unicorn-card__bloc-photo">
            <unicorn-picture :unicorn="unicorn" medium/>
        </div>
        <div class="unicorn-card__name">
            Nom : <span>{{ unicorn.name }}</span>
        </div>
        <div class="unicorn-card__button">
            <unicorn-button :to="to">Voir plus</unicorn-button>
        </div>
    </div>
</template>
<script>
import UnicornButton from '@/components/UnicornButton'
import UnicornPicture from '@/components/UnicornPicture.vue'
export default {
    name: 'UnicornCard',
    components: {
        UnicornButton,
        UnicornPicture
    },
    props: {
        unicorn: {
            type: Object,
            required: true
        }
    },
    computed: {
        to () {
            return `/${this.unicorn.id}`
        }
    }
}
</script>
<style scoped>
.unicorn-card {
  min-width: 200px;
  background-color: aliceblue;
  border-radius: 15px;
  border: 1px solid #7EA8EF;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.unicorn-card__bloc-photo {
  text-align: center;
}

.unicorn-card__name {
  text-align: center;
  font-weight: bold;
}

.unicorn-card__name span {
  font-weight: normal;
}

.unicorn-card__button {
  margin: 20px 0;
  text-align: center;
}
</style>
