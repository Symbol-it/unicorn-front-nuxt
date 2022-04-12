<template>
    <div class="formulaire-unicorn">
        <span>
            <span class="formulaire-unicorn__title" v-if="isEditing">
                Modifie {{ unicorn.name }}
            </span>
            <label for="picture">
                <unicorn-picture small :unicorn="form" :preview="image"/>
            </label>
        </span>
        <form>
            <label for="name" class="formulaire-unicorn__label--display">Nom</label>
            <input 
                type="text" 
                name="name" 
                id="name" 
                autocomplete="off" 
                v-model="form.name" 
                class="formulaire-unicorn__input formulaire-unicorn__input--display"> 
            <label for="birthyear" class="formulaire-unicorn__label--display">Année de naissance</label> 
            <input 
                type="text" 
                name="birthyear" 
                id="birthyear" 
                autocomplete="off" 
                v-model="form.birthyear" 
                class="formulaire-unicorn__input"> 
            <label for="weight" class="formulaire-unicorn__label--display">Poids</label> 
            <input 
                type="text" 
                name="weight" 
                id="weight" 
                autocomplete="off" 
                v-model="form.weight" 
                class="formulaire-unicorn__input"> 
            <label for="hobbies" class="formulaire-unicorn__label--display">Hobbies</label> 
            <input 
                type="text" 
                name="hobbies" 
                id="hobbies" 
                autocomplete="off" 
                v-model="form.hobbies" 
                class="formulaire-unicorn__input"> 

            <div class="formulaire-unicorn__capacities">
                <div class="formulaire-unicorn__capacities__items" v-for="(cap,index) in capacities" :key="index"> 
                    <input type="checkbox" class="formulaire-unicorn__capacities__items__input" :id="cap.label" :value="cap" v-model="form.capacities"> 
                    <label :for="cap.label" class="formulaire-unicorn__capacities__items__label"> {{ cap.label }} </label>
                </div>
            </div>
            <label for="picture" class="formulaire-unicorn__label--display">{{ txtPicture }}</label> 
            <input 
                type="file" 
                class="formulaire-unicorn__input-file" 
                id="picture"
                @change="editImage"
                name="files" 
                accept="image/png, image/jpeg">
            <hr> 
            <input 
                type="submit" 
                @click.prevent="actSubmit" 
                class="formulaire-unicorn__input-button" 
                :value="submitActionName">
        </form>
    </div>
</template>
<script>

export default{
    name: "FormulaireUnicorn",
    props: {
        unicorn: {
            type: Object,
            required: false
        },
        submitActionName: {
            type: String,
            default: "Envoyer"
        },
        txtPicture: {
            type: String,
            default: "Image"
        },
        capacities: {
            type: Array
        }
    },
    data() {
        return {
            form:{
                name: this.unicorn?.name || '',
                birthyear: this.unicorn?.birthyear || '',
                weight: this.unicorn?.weight || '',
                hobbies: this.unicorn?.hobbies || '',
                photo: this.unicorn?.photo || null,
                capacities: this.unicorn?.capacities || []
            },

            image: ''
        }
    },
    computed: {
        isEditing(){
            return this.submitActionName === 'modifier'
        }
    },
    methods: {
        actSubmit() {
            this.$emit("act", this.form)
        },
        editImage(e){
            this.image = URL.createObjectURL(e.target.files[0])
        }
    }
}
</script>
<style scoped>

.formulaire-unicorn__label--display{
    display: block;
}

.formulaire-unicorn__input-file{
    padding: 5px;
}

.formulaire-unicorn__input{
    padding: 10px 20px;
    margin: 5px 5px 10px 5px;
}
.formulaire-unicorn__span-capacities{
    display:block;
}

.formulaire-unicorn__span-capacities__label{
    text-align: center;
    display: inline-block;
    width: 150px;
    margin: 5px 0 5px 0;
    padding: 15px 0 15px 0;
    border-radius: 16px;
    cursor: pointer;
    color: white;
}

.formulaire-unicorn__span-capacities__label:hover{
    box-shadow: inset 0px -4px 0px rgba(255, 255, 255, 0.25);
    transition: box-shadow 0.5s;
}

.formulaire-unicorn__span-capacities__input:checked + .formulaire-unicorn__span-capacities__label{
    background-color: green;
}


.formulaire-unicorn__span-capacities__input{
    display: none;
}

.formulaire-unicorn__span-capacities__input + .formulaire-unicorn__span-capacities__label{
    background-color: red;
}

.formulaire-unicorn__capacities__items__label{
    text-align: center;
    display: inline-block;
    width: 150px;
    margin: 5px 0 5px 0;
    padding: 15px 0 15px 0;
    border-radius: 16px;
    cursor: pointer;
    color: white;
}

.formulaire-unicorn__capacities__items__label:hover{
    box-shadow: inset 0px -4px 0px rgba(255, 255, 255, 0.25);
    transition: box-shadow 0.5s;
}

.formulaire-unicorn__capacities__items__input:checked + .formulaire-unicorn__capacities__items__label{
    background-color: green;
}


.formulaire-unicorn__capacities__items__input{
    display: none;
}

.formulaire-unicorn__capacities__items__input + .formulaire-unicorn__capacities__items__label{
    background-color: red;
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
    letter-spacing: 5px;
    text-indent: 5px;
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
    margin: 10px;
}

.formulaire-unicorn__input-button:hover {
    background: #7EA8EF;
    border: 2px solid black;
    box-shadow: inset -4px -4px 0px rgba(255, 255, 255, 0.25);
}

.formulaire-unicorn__title{
    margin-right: 10%;
}
</style>
