<template>
  <div class="unicorn">
    <unicorn-picture class="picture-unicorn__photo" :unicorn="unicorn" />
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
      <button class="unicorn__actions__button" @click="openConfirmationDelete">
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
import DeleteModal from "@/components/DeleteModal";
import UnicornPicture from '@/components/UnicornPicture.vue';
export default {
  name: 'UnicornDetail',
  components: { DeleteModal, UnicornPicture },
  data () {
    return {
      showConfirmationDelete: false,
    }
  },

  async asyncData ({ params, error, $http }) {
    const unicornId = params.id
    
    try{
      const unicorn = await $http.$get(process.env.baseUrl + '/unicorns/' + unicornId)
      return { unicorn }
    }
    catch (err){
      error({ statusCode: 500, message: 'La licorne n\'existe pas' })
    }
    
  },

  methods: {
    openConfirmationDelete () {
      this.showConfirmationDelete = true
    },
    cancelDeleteUnicorn () {
      this.showConfirmationDelete = false
    },
    async deleteUnicorn () {
      try{
        const name = this.unicorn.name;
        await this.$http.$delete(process.env.baseUrl + '/unicorns/' + this.unicorn.id)
        this.showConfirmationDelete = false
        await this.$router.push('/')
        this.$toast.success('Unicorn ' + name + ' a été supprimé').goAway(2500)
      }
      catch(e){
        this.$toast.error('Problème dans la suppresion de la licorne')
      }
    },
    updateUnicorn() {
      this.$router.push(`/update/${this.unicorn.id}`)
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

.picture-unicorn__photo{
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
