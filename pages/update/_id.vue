<template>
    <div class="update-id">
        <span> 
            Modifie {{ unicorn.name }}
            <unicorn-picture small :unicorn="unicorn"/>
        </span>
        <formulaire-unicorn 
            txtPicture="Nouvelle Image" 
            :unicorn="unicorn" 
            submitActionName="modifier" 
            @act="editUnicorn"/>
    </div>
</template>
<script>
import UnicornPicture from '@/components/UnicornPicture.vue'
import FormulaireUnicorn from '@/components/FormulaireUnicorn.vue'
export default {
  components: { UnicornPicture, FormulaireUnicorn },
    name: "Update",
    async asyncData({ params, error, $http }){
        const {id} = params
        try{
            const unicorn = await $http.$get(process.env.baseUrl + '/unicorns/' + id)
            return { unicorn }
        }
        catch{
            error({statutCode:500, message:'Impossible de trouver la licorne'})
        }
    },

    methods: {
        async editUnicorn(form){
            try{
                let file = document.querySelector(".formulaire-unicorn__input-file");
                if(file.value){
                    await this.$http.$post(process.env.baseUrl + "/upload", new FormData(document.querySelector('form')))
                    const taille = await this.$http.$get(process.env.baseUrl + "/upload/files/count").then( valeur => { return valeur })
                    const newUrl = await this.$http.$get(process.env.baseUrl + "/upload/files/").then(valeur => { return valeur })
                    const newPhoto = newUrl[taille-1]
                    form.photo = newPhoto
                }
                await this.$http.$put(process.env.baseUrl + "/unicorns/"+this.unicorn.id, form)
                this.$toast.success('Unicorn ' + form.name + ' a été modifié avec succès').goAway(2500)
                this.$router.go(-1)
            }
            catch(e){
                this.$toast.error("Problème dans la modification de la licorne").goAway(2500)
            }
        }
    }
}
</script>
<style scoped>
.update-id{
    width: 400px;
    text-align: center;
    margin: auto;
    font-weight: bold;
    font-size: 20px;
    border: 2px solid #7EA8EF;
    border-radius: 15px;
    margin-bottom: 0.50em;
}
</style>
