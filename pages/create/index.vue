<template>
    <div class="add-unicorn">
        <formulaire-unicorn 
            submitActionName="ajouter" 
            @act="addUnicorn" 
            class="add-unicorn__formulaire"/>
    </div>
</template>
<script>
export default{
    methods: {
        async addUnicorn(form){
            try {
                let file = document.querySelector(".formulaire-unicorn__input-file")
                if(file.value){
                    await this.$http.$post(process.env.baseUrl + "/upload", new FormData(document.querySelector('form')))
                    const taille = await this.$http.$get(process.env.baseUrl+"/upload/files/count").then( valeur => { return valeur })
                    const newUrl = await this.$http.$get(process.env.baseUrl+"/upload/files/").then(valeur => { return valeur })
                    const newPhoto = newUrl[taille-1]
                    form.photo = newPhoto
                }
                await this.$http.$post(process.env.baseUrl + "/unicorns/", form)
                this.$router.go(-1)
                this.$toast.success('La ' + form.name + ' a été créée avec succès ').goAway(2500)
            }
            catch(e){
                this.$toast.error('Problème dans la création de la licorne').goAway(2500)
            }
        }
    }
}
</script>
<style scoped>

.add-unicorn{
    width: 400px;
    text-align: center;
    margin: auto;
    font-weight: bold;
    font-size: 20px;
    border: 2px solid #7EA8EF;
    border-radius: 15px;
    margin-bottom: 0.50em;
}

.add-unicorn__formulaire{
    padding-top: 15px;
}
</style>
