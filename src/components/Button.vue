<template>
    <button v-on:click = "onClick()" class="btn" :style="{background:color}">{{text}}</button>
</template>

<script>


export default{

    name: 'Button',
    
    props:{
        text: String,
        color: String,
    },

    methods:{
        onClick(){
            this.$emit('btn-click')
        }
    }
 }

    
    
</script>

<style scoped>
    
</style>