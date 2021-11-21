<template>
    <div :key="task.id" v-for="task in tasks">
        <TaskVue @delete-task="deleteTask(task.id)" @toggle-reminder="toggleReminder(task.id)" :task="task"/>
        
    </div>
</template>

<script>
import TaskVue from './Task.vue'
    

    
    export default{
        name: "Tasks",

        components:{
            TaskVue
        },

        props : {
            tasks : Array
        },

        methods:{
            toggleReminder(id){
                this.$emit('toggle-reminder',id)
            },

            deleteTask(id){
                this.$emit('delete-task',id)
            }
        }
        
    }

    
</script>

<style scoped>
    h3{
        color:red;
        text-align: left;
    }
</style>>

