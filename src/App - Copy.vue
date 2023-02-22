<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
    <!-- <div v-if="showAddTask"> -->
    <!-- <div v-show="showAddTask">
      <AddTask @toggle-add-task="toggleAddTask" @add-task="addTask" />
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" /> -->
    <!-- <router-view></router-view> -->
    <router-view :showAddTask="showAddTask"></router-view>
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer'
// import Tasks from './components/Tasks'
// import AddTask from './components/AddTask'


export default {
  name: 'App',
  components: {
    Header,
    Footer,
    // Tasks,
    // AddTask,
  },

  data() {
    return {
      // tasks: [],
      showAddTask: false
    }
  },

  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    
  //   // addTask(task) {
  //   //   this.tasks = [...this.tasks, task]
  //   // },
  //   async addTask(task) {
  //     // Send the insert (POST) to the db.json
  //     const response = await fetch('api/tasks', {
  //       method: 'POST',
  //       headers: {
  //         'Content-type': 'application/json',
  //       },
  //       body: JSON.stringify(task)
  //     })

  //     // Convert the response to JSON and add it to the tasks
  //     const data = await response.json()
  //     this.tasks = [...this.tasks, data]
  //   },

  //   // deleteTask(id) {
  //   //   if (confirm('Are you sure?')) {
  //   //     this.tasks = this.tasks.filter((task) => task.id !== id)
  //   //   }
  //   // },
  //   async deleteTask(id) {
  //     if (confirm('Are you sure?')) {
  //       // Send the delete to the JSON backend server
  //       const response = await fetch(`api/tasks/${id}`, {
  //         method: 'DELETE'
  //       })


  //       // response.status === 200 ? 
  //       //     (this.tasks = this.tasks.filter((task) => task.id !== id)) : 
  //       //     alert('Error deleting task')

  //       if (response.status === 200)
  //         this.tasks = this.tasks.filter((task) => task.id !== id)
  //       else
  //         alert('Error deleting task')
  //     }
  // },

  //   // toggleReminder(id) {
  //   //   this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder} : task)
  //   // },

  //   async toggleReminder(id) {
  //     // Get the task to toggle
  //     const taskToToggle = await this.fetchTask(id)
  //     const updatedTask = {...taskToToggle, reminder: !taskToToggle.reminder}

  //     // Update the task using the PUT method of the JSON backend server
  //     const response = await fetch(`api/tasks/${id}`, {
  //       method: 'PUT',
  //       headers: {
  //         'Content-type': 'application/json'
  //       },
  //       body: JSON.stringify(updatedTask)
  //     })

  //     // Get the response from the backend
  //     const data = await response.json()

  //     // Update the tasks with the information returned by the JSON backend server
  //     this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder} : task)
  //   },

  //   async fetchTasks() {
  //     // Request to JSON backend server the tasks

  //     // const response = await fetch('http://localhost:5000/tasks')
  //     const response = await fetch('api/tasks')   // After configuring vue.config.js we can use api
  //     const data = await response.json()
  //     return data
  //   },

  //   async fetchTask(id) {
  //     // Request to JSON backend server the task id

  //     // const response = await fetch(`http://localhost:5000/tasks/${id}`)
  //     const response = await fetch(`api/tasks/${id}`)   // After configuring vue.config.js we can use api
  //     const data = await response.json()
  //     return data
  //   },

  },

  // async created() {
  //   // this.tasks = [
  //   //   {
  //   //     id: 1,
  //   //     text: 'Doctors Appointment',
  //   //     day: 'March 1st at 2:30pm',
  //   //     reminder: true
  //   //   },
  //   //   {
  //   //     id: 2,
  //   //     text: 'Meeting at School',
  //   //     day: 'March 3rd at 1:30pm',
  //   //     reminder: true
  //   //   },
  //   //   {
  //   //     id: 3,
  //   //     text: 'Food Shopping',
  //   //     day: 'March 3rd at 11:00am',
  //   //     reminder: false
  //   //   },
  //   // ]

  //   // Populate the tasks array using the JSON backend
  //   this.tasks = await this.fetchTasks()
  // },

}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swqp');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
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

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}

</style>
