<template>
    <div class="update-id">
        <span> 
            Editing {{ unicorn.name }} &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
            <picture-found v-show="!pictureSelected" class="update-id__picture-found" :unicorn="unicorn"/>
            <img v-show="pictureSelected" class="update-id__label__photo"/>
        </span>
        <formulaire-unicorn :txtPicture="txtPicture" :unicorn="unicorn" :valeur="edit" @act-submit="editUnicorn" @act-upload="previewPicture"/>
    </div>
</template>
<script>
import PictureFound from '../../components/PictureFound.vue';
import FormulaireUnicorn from '../../components/FormulaireUnicorn.vue';
export default {
  components: { PictureFound, FormulaireUnicorn },
    name: "Update",
    data(){
        return {
            pictureSelected: false
        }
    },
    async asyncData( { params, error, $http }){
        const {id} = params
        try{
            const unicorn = await $http.$get('http://localhost:1337/unicorns/' + id);
            return { unicorn }
        }
        catch{
            error({statutCode:404});
        }
    },

    computed:{
        edit(){
            return "edit";
        },
        txtPicture(){
            return "New Picture";
        }
    },

    methods: {
        async editUnicorn(){
            let object = {};
            let elm = document.getElementsByTagName("input");
            for( let i = 0; i<elm.length;i++){
                if(elm[i].value !== "" && elm[i].type != 'file') object[elm[i].name] = elm[i].value;
                if(elm[i].name == 'hobbies') object[elm[i].name] = elm[i].value;
            }
            if(elm[4].value !== ""){
                await this.$http.$post("http://localhost:1337/upload", new FormData(document.querySelector('form'))); // <input file> doit avoir le name : files
                const taille = await this.$http.$get("http://localhost:1337/upload/files/count").then( valeur => {return valeur; });
                const newUrl = await this.$http.$get("http://localhost:1337/upload/files/").then(valeur => { return valeur; });
                const newPhoto = newUrl[taille-1];
                object['photo'] = newPhoto;
            }

            await this.$http.$put("http://localhost:1337/unicorns/"+this.unicorn.id, object);
            this.$router.go(-1);
            alert("Unicorn edit with success !");
        },

        previewPicture(){
            let inputFile = document.querySelector(".formulaire-unicorn__input-file");
            inputFile.onchange = () => {
                this.pictureSelected = true;
                let img = document.querySelector(".update-id__label__photo");
                img.src = URL.createObjectURL(inputFile.files[0]);
            };
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

.update-id__label__photo{
    width:100px;
    height: 100px;
    border-radius: 100%;
    vertical-align: middle;
    padding-top: 0.5em;
}


</style>
