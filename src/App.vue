<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>
  <div class="container">
  <Header @toggle-add-task="toggleAddTask" text="Task Tracker"
  :showAddTask="showAddTask"/>
  <TasksVue @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks" />
  </div>
  <router-view/>
</template>

<script>
    import Header from './components/Header.vue'
    import TasksVue from './components/Tasks.vue'

    export default{
      name: 'App',
      
      components: {
      Header,
      TasksVue
    },

    data(){
      return { 
        tasks : [],
        showAddTask: false
      }
        
    },

    methods:{
      toggleAddTask(){
        this.showAddTask = !this.showAddTask
      },

      deleteTask(id){
        this.tasks = this.tasks.filter((task) => task.id !== id)
      },

      toggleReminder(id){
        this.tasks = this.tasks.map((task) => task.id === id ? {...task,reminder: !task.reminder}: task)
        
      }
    },
    
    created(){
        this.tasks = 
          [
          {
            id: "1",
            text:"text 1",
            reminder : true,
            date : "date 1"
          },

          {
            id : "2",
            text:"text 2",
            reminder : false,
            date : "date 2"
          },

          {
            id : "3",
            text:"text 3",
            reminder : false,
            date : "date 3"
          }
        ]
        
    }
    }
</script>


<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }

    .btn {
      display: inline-block;
      background: #000;
      color: #fff;
      border: none;
      padding: 10px 20px;
      margin: 5px;
      border-radius: 5px;
      cursor: pointer;
      text-decoration: none;
      font-size: 15px;
      font-family: inherit;
    }

    .btn-block {
        display: block;
        width: 100%;
    }

    .container {
        max-width: 500px;
        margin: 30px auto;
        overflow: auto;
        min-height: 300px;
        border: 1px solid steelblue;
        padding: 30px;
        border-radius: 5px;
        }
</style>
