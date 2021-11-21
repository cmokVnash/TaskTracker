<template>
    <div  @dblclick="toggleReminder(task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
    <h3>
            {{task.text}}  
            <i @click="deleteTask(task.id)" class="fas fa-trash-alt"></i>
            
    </h3>
        <p>{{task.date}}</p>
    
    </div>
</template>

<script>
    export default{
        name: "Task",

        props:{
            task : Object
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
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.task p{
    display: flex;
  align-items: flex-end;
  justify-content: space-between;
}
     
</style>