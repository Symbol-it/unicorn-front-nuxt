<template>
    <div class="formulaire-unicorn">
        <label for="name" class=""> Name </label><br/>
        <input type="text" name="name" id="name" autocomplete="off" :placeholder="unicorn.name" class="formulaire-unicorn__input"> <br/>
        <label for="birthyear"> Birthyear </label> <br/>
        <input type="text" name="birthyear" id="birthyear" autocomplete="off" :placeholder="unicorn.birthyear" class="formulaire-unicorn__input"> <br/>
        <label for="weight"> Weight </label> <br/>
        <input type="text" name="weight" id="weight" autocomplete="off" :placeholder="unicorn.weight" class="formulaire-unicorn__input"> <br/>
        <label for="hobbies"> Hobbies </label> <br/>
        <input type="text" name="hobbies" id="hobbies" autocomplete="off" :value="unicorn.hobbies" class="formulaire-unicorn__input"> <br/>
        <label for="picture"> {{ txtPicture }} </label> <br/>
        <form>
            <input type="file" class="formulaire-unicorn__input-file formulaire-unicorn__input-file--padding" name="files" accept="image/png, image/jpeg">
            <hr> 
            <input type="submit" @click="actSubmit" class="formulaire-unicorn__input-button" :value="valeur">
        </form>
    </div>
</template>
<script>

export default{
    name: "FormulaireUnicorn",
    props: {
        unicorn: {
            type: Object,
            default: () => {return {name: "", birthyear: "", weight: "", hobbies: "", photo: null};}
        },
        valeur: {
            type: String,
            default: "Envoyer"
        },
        txtPicture: {
            type: String,
            default: "Picture"
        }
    },

    methods: {
        actSubmit(e) {
            e.preventDefault();
            this.$emit("act");
        }
    }
}
</script>
<style scoped>

.formulaire-unicorn__input-file--padding{
    padding: 5px;
}
/*.formulaire-unicorn__input-file::-webkit-file-upload-button, .formulaire-unicorn__input-file::file-selector-button{
    min-height: 50px;
    min-width: 150px;
    font-weight: 400px;
    font-size: 14px;
    line-height: 18px;
    background: #7EA8EF;
    border: 2px solid black;
    border-radius: 16px;
    color: black;
    text-decoration: none;
    cursor: pointer;
    transition: 0.3s;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    text-transform: uppercase;
    margin: auto;
    margin: 10px;
}

.formulaire-unicorn__input-file::-webkit-file-upload-button:hover{
    background: #7EA8EF;
    border: 2px solid black;
    box-shadow: inset -4px -4px 0px rgba(255, 255, 255, 0.25);
}*/

.formulaire-unicorn__input{
    padding: 10px 20px;
    margin: 5px;
    margin-bottom: 10px;
}

hr {
    width: 75%;
    color: #7EA8EF
}
.formulaire-unicorn__input-button {
    min-height: 50px;
    min-width: 150px;
    font-weight: 400px;
    font-size: 14px;
    letter-spacing: 18px;
    text-indent: 18px;
    line-height: 18px;
    background: #7EA8EF;
    border: 2px solid black;
    border-radius: 16px;
    color: black;
    text-decoration: none;
    cursor: pointer;
    transition: 0.3s;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    text-transform: uppercase;
    margin: auto;
    margin: 10px;
}

.formulaire-unicorn__input-button:hover {
    background: #7EA8EF;
    border: 2px solid black;
    box-shadow: inset -4px -4px 0px rgba(255, 255, 255, 0.25);
}
</style>
