<template>
        <img :class="['unicorn-picture', {'unicorn-picture--small' : small, 'unicorn-picture--medium' : medium }]" :src="srcImage">
</template>
<script>
    export default{
        name: "UnicornPicture",
        props:{
            unicorn: {
                type: Object,
                required: true
            },
            small: {
                type: Boolean,
                default: false
            },
            medium: {
                type: Boolean,
                default: false
            }
        },
        computed:{
            srcImage(){
                if(this.unicorn.photo) return process.env.baseUrl + this.unicorn.photo.url
                return require('~/assets/icons/not-found-image.jpg')
            }
        }
    }
</script>
<style scoped>

.unicorn-picture{
    height: 300px;
    width: 300px;
    object-fit: cover;
    border-radius: 100%;
}

.unicorn-picture--small{
    margin-top: 15px;
    border-radius: 100%;
    width: 100px;
    height: 100px;
    object-fit: cover;
    object-position: center;
    display:inline;
    vertical-align: middle;
}

.unicorn-picture--medium{
    margin-top: 15px;
    border-radius: 100%;
    width: 144px;
    height: 144px;
    object-fit: cover;
    object-position: center;
    display:inline;
    vertical-align: middle;
}

.unicorn-picture--small{
    margin-top: 15px;
    margin-left: 10%;
    border-radius: 100%;
    width: 100px;
    height: 100px;
    object-fit: cover;
    object-position: center;
    display:inline;
    vertical-align: middle;
}
</style>