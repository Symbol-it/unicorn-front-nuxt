<template>
    <div class="item" @click="goToMenuItem">
        <h1 class="item__title"> {{ item.nom }} </h1>
    </div>
</template>
<script>
export default {
    name:"ItemMenu",
    props:{
        item:{
            type: Object,
            required: true
        }
    },

    methods:{
        goToMenuItem(){
            this.$emit("redirection", this.item.url)
        }
    }
}
</script>
<style scoped>
.item__title{
    text-align: center;
    cursor: pointer;
    padding: 5px 0 5px 0;
}
</style>
