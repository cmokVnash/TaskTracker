<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>
  <div class="container">
  <Header @toggle-add-task="toggleAddTask" text="Task Tracker"
  :showAddTask="showAddTask"/>
  <div v-show="showAddTask">
        <AddTask @add-task="addTask"/>
    </div>
  <TasksVue @delete-task="deleteTask" @toggle-reminder="toggleReminder" :tasks="tasks" />
  </div>
  <router-view/>
</template>

<script>
    import Header from './components/Header.vue'
    import TasksVue from './components/Tasks.vue'
    import AddTask from './components/AddTask.vue'

    export default{
      name: 'App',
      
      components: {
      Header,
      TasksVue,
      AddTask
    },

    data(){
      return { 
        tasks : [],
        showAddTask: false
      }
        
    },

    methods:{

     async addTask(task){

       const res = await fetch('api/tasks', {
         method: 'POST',
         headers: {
           'Content-type' : 'application/json',
           
         },
         body: JSON.stringify(task)
       })

       const data = await res.json()
        this.tasks = [...this.tasks, data]
      },

      toggleAddTask(){
        this.showAddTask = !this.showAddTask
      },

      async deleteTask(id){
        if(confirm('ARE YOU SURE?')){
          const res = await fetch(`api/tasks/${id}`,{
            method: 'DELETE'
          })

          res.status === 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert('ERROR deleting task')

          
        }

        
      },

      async toggleReminder(id){

        const taskToToggle = await this.fetchTask(id)

        const updTask = {...taskToToggle, reminder: !taskToToggle.reminder}

        
        const res = await fetch(`api/tasks/${id}`, {
          method: 'PUT',
          headers: {
            'Content-type': 'application/json'
          },
          body: JSON.stringify(updTask)
        })

        const data = await res.json()

        this.tasks = this.tasks.map((task) => task.id === id ? {...task,reminder: data.reminder}: task)
        
      },

      async fetchTasks(){
        const res = await fetch('api/tasks')
        console.log("In Fetch")
        const data = await res.json();
        
        return data
      },

      async fetchTask(id){
        const res = await fetch(`api/tasks/${id}`)
        console.log("In Fetch")
        const data = await res.json();
        
        return data
      },
    },

      
    
    async created(){
        this.tasks = await this.fetchTasks()
        console.log("in created")
        //   [
        //   {
        //     id: "1",
        //     text:"text 1",
        //     reminder : true,
        //     date : "date 1"
        //   },

        //   {
        //     id : "2",
        //     text:"text 2",
        //     reminder : false,
        //     date : "date 2"
        //   },

        //   {
        //     id : "3",
        //     text:"text 3",
        //     reminder : false,
        //     date : "date 3"
        //   }
        // ]
        
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
