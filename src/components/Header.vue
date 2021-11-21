<template>
    
    <div class="header">
        <h1>{{text}}</h1>
        <Button 
        @btn-click = "onClick()"
        :color="showAddTask ? 'red' : 'green'" :text="showAddTask ? 'Close' : 'Open'"/>

        
    </div>
    <div v-show="showAddTask">
        <AddTask />
    </div>
        
    
</template>

<script>

    import Button from './Button.vue'
    import AddTask from './AddTask.vue'
    export default{

        name: 'Header',

        components:{
            Button,
            AddTask
        },
        props: {
            text: String,
            showAddTask: Boolean
        },

        methods:{
            onClick(){
                this.$emit('toggle-add-task')
            }
        }
        
    }
</script>

<style scoped>
    .header{
        max-width: 500px;
        display: flex;
        justify-content: space-between;
        margin: 0 50px;
    }

    
</style>