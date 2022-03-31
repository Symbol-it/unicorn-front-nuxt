<template>
<div class="picture-unicorn">
    <img v-if="found" class="picture-unicorn__photo" :src="srcImage">
    <img v-else class="picture-unicorn__photo" src="~assets/icons/not-found-image.jpg">
</div>
</template>
<script>
    export default{
        name: "PictureFound",
        props:{
            unicorn: {
                type: Object,
                required: true
            }
        },
        computed:{
            found(){
                return this.unicorn.photo != null;
            },

            srcImage(){
                return "http://localhost:1337" + this.unicorn.photo.url;
            }
        }
    }
</script>
<style scoped>
.picture-unicorn__photo{
  height: 300px;
  width: 300px;
  object-fit: cover;
  border-radius: 100%;
}

.unicorn-card__bloc-photo__image img{
  margin-top: 15px;
  border-radius: 100%;
  width: 144px;
  height: 144px;
  object-fit: cover;
  object-position: center;
}

.update-id__picture-found{
    display: inline;
}
.update-id__picture-found img{
    width:100px;
    height: 100px;
    border-radius: 100%;
    vertical-align: middle;
    padding-top: 0.5em;
}
</style>