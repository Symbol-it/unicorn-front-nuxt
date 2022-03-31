<template>
    <div class="add-unicorn">
        <formulaire-unicorn :valeur="add" @act="addUnicorn" class="add-unicorn__formulaire-unicorn--padding-top"/>
    </div>
</template>
<script>
export default{
    async asyncData( { error, $http }){
        try{
            const unicorn = await $http.$get('http://localhost:1337/unicorns/1');
            return { unicorn }
        }
        catch{
            error({statutCode:404});
        }
    },

    computed:{
        add(){
            return "add";
        }
    },
    methods: {
        async addUnicorn(){
            let object = {};
                let elm = document.getElementsByTagName("input");
                for( let i = 0; i<elm.length;i++){
                    if(elm[i].value !== "" && elm[i].type != 'file') object[elm[i].name] = elm[i].value;
                }
                if(elm[4].value !== ""){
                    await this.$http.$post("http://localhost:1337/upload", new FormData(document.querySelector('form'))); // input file doit avoir le name : files
                    const taille =await this.$http.$get("http://localhost:1337/upload/files/count").then( valeur => {return valeur; });
                    const newUrl = await this.$http.$get("http://localhost:1337/upload/files/").then(valeur => { return valeur; });
                    const newPhoto = newUrl[taille-1];
                    object['photo'] = newPhoto;
                }

                await this.$http.$post("http://localhost:1337/unicorns/", object);
                this.$router.go(-1);
                alert("Unicorn add with success !");
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

.add-unicorn__formulaire-unicorn--padding-top{
    padding-top: 15px;
}
</style>
