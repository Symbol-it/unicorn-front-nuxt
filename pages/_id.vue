<template>
  <div class="unicorn">
    <img class="unicorn__photo" :src="photoUnicornUrl" alt="Photo de la licorne">
    <ul class="unicorn__details">
      <li>
        <span class="unicorn__details__label">Nom :</span>
        {{ unicorn.name }}
      </li>
      <li>
        <span class="unicorn__details__label">Année de naissance :</span>
        {{ unicorn.birthyear }}
      </li>
      <li>
        <span class="unicorn__details__label">Poids :</span>
        {{ unicorn.weight }} kg
      </li>
      <li>
        <span class="unicorn__details__label">Hobbies :</span>
        {{ unicorn.hobbies }}
      </li>
    </ul>
    <div class="unicorn__actions">
      <button class="unicorn__actions__button" @click="openConfimartionDelete">
        Supprimer
      </button>
      <button class="unicorn__actions__button" @click="updateUnicorn">
        Modifier
      </button>
      <delete-modal :open="showConfirmationDelete"
                    @cancel="cancelDeleteUnicorn"
                    @confirm-delete="deleteUnicorn">
        Êtes-vous sur de vouloir supprimer {{ unicorn.name }} ? 😢
      </delete-modal>
    </div>
  </div>
</template>
<script>
import DeleteModal from "../components/DeleteModal";
export default {
  name: 'UnicornDetail',
  components: {DeleteModal},
  data () {
    return {
      showConfirmationDelete: false,
    }
  },

  async asyncData ({ params, $http }) {
    const unicornId = params.id
    const unicorn = await $http.$get('http://localhost:1337/unicorns/' + unicornId)
    return { unicorn }
  },

  computed: {
    photoUnicornUrl () {
      return 'http://localhost:1337' + this.unicorn.photo.url
    }
  },

  methods: {
    openConfimartionDelete () {
      this.showConfirmationDelete = true
    },
    cancelDeleteUnicorn () {
      this.showConfirmationDelete = false
    },
    async deleteUnicorn () {
      await this.$http.$delete('http://localhost:1337/unicorns/' + this.unicorn.id)
      this.showConfirmationDelete = false
      await this.$router.push('/')
    },
    updateUnicorn() {
      this.$router.push('/update')
    }
  }
}
</script>
<style scoped>
.unicorn {
  padding: 30px;
  border: 2px solid #7EA8EF;
  border-radius: 16px;
  text-align: center;
  font-size: 20px;
  max-width: 800px;
  margin: auto;
}

.unicorn__photo {
  height: 300px;
  width: 300px;
  object-fit: cover;
  border-radius: 100%;
}

.unicorn__details {
  list-style: none;
  padding: 0;
  display: grid;
  row-gap: 20px;
}

.unicorn__details__label {
  font-weight: bold;
}

.unicorn__actions__button {
  background-color: #CFE2F3;
  border-radius: 8px;
  border: 1px solid #000000;
  padding: 15px 20px;
  font-size: 14px;
  margin: 10px;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.unicorn__actions__button:hover {
  background-color: #C9DAF8;
  cursor: pointer;
}
</style>
