<template>
    <form @submit="onSubmit" action="">
        <label for="">Text </label>
        <input type="text" v-model='text'><br>

        <label for="">Date </label>
        <input type="text" v-model="date"><br>

        <label for="">Reminder </label>
        <input type="checkbox" v-model="reminder"><br>

        
        <input type="Submit" ><br>
    </form>
</template>

<script>
    export default{
        name: "AddTask",

        data(){
            return{
                text : '',
                date : '',
                reminder : false,
                 }
        },

        methods:{
            onSubmit(e) {
                e.preventDefault()

                if(!this.text){
                    alert('Please add a task')
                    return
                }

                const newTask = {
                    //id: Math.floor(Math.random() * 100000),
                    text: this.text,
                    date: this.date,
                    reminder: this.reminder
                }

                this.$emit('add-task',newTask)

                this.text = '',
                this.date = '',
                this.reminder = ''
            }
        }

        

    }
</script>

<style scoped>

</style>