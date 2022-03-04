<template>
    <div class="unicorn-list">
        <unicorn-card v-for="(unicorn, index) in unicorns" :unicorn="unicorn" :key="index"/>
    </div>
</template>
<script>
import UnicornCard from '@/components/UnicornCard'
export default {
    name: 'UnicornList',
    components: {
        UnicornCard
    },
    props: {
        unicorns: {
            type: Array,
            required: true
        }
    }
}
</script>
<style>
.unicorn-list {
    display: grid;
    grid-template-columns: repeat(5, minmax(0, 1fr));
    column-gap: 16px;
    row-gap: 32px;
}
</style>
