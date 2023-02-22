<template>
    <div v-show="showAddTask">
      <!-- <AddTask @toggle-add-task="toggleAddTask" @add-task="addTask" /> -->
      <AddTask @add-task="addTask" />
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
</template>

<script>

import Tasks from '../components/Tasks'
import AddTask from '../components/AddTask'

export default {
    name: 'Home',
    props: {
        showAddTask: Boolean
    },
    components: {
        Tasks,
        AddTask,
    },

    data() {
        return {
            tasks: [],
        }
    },

    methods: {
        async addTask(task) {
            // Send the insert (POST) to the db.json
            const response = await fetch('api/tasks', {
                method: 'POST',
                headers: {
                    'Content-type': 'application/json',
                },
                body: JSON.stringify(task)
            })

            // Convert the response to JSON and add it to the tasks
            const data = await response.json()
            this.tasks = [...this.tasks, data]
        },

        async deleteTask(id) {
            if (confirm('Are you sure?')) {
                // Send the delete to the JSON backend server
                const response = await fetch(`api/tasks/${id}`, {
                    method: 'DELETE'
                })


                // response.status === 200 ? 
                //     (this.tasks = this.tasks.filter((task) => task.id !== id)) : 
                //     alert('Error deleting task')

                if (response.status === 200)
                    this.tasks = this.tasks.filter((task) => task.id !== id)
                else
                    alert('Error deleting task')
            }
        },

        async toggleReminder(id) {
            // Get the task to toggle
            const taskToToggle = await this.fetchTask(id)
            const updatedTask = {...taskToToggle, reminder: !taskToToggle.reminder}

            // Update the task using the PUT method of the JSON backend server
            const response = await fetch(`api/tasks/${id}`, {
                method: 'PUT',
                headers: {
                    'Content-type': 'application/json'
                },
                body: JSON.stringify(updatedTask)
            })

            // Get the response from the backend
            const data = await response.json()

            // Update the tasks with the information returned by the JSON backend server
            this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder} : task)
        },

        async fetchTasks() {
            // Request to JSON backend server the tasks

            // const response = await fetch('http://localhost:5000/tasks')
            const response = await fetch('api/tasks')   // After configuring vue.config.js we can use api
            const data = await response.json()
            return data
        },

        async fetchTask(id) {
            // Request to JSON backend server the task id

            // const response = await fetch(`http://localhost:5000/tasks/${id}`)
            const response = await fetch(`api/tasks/${id}`)   // After configuring vue.config.js we can use api
            const data = await response.json()
            return data
        },
  },

  async created() {
    this.tasks = await this.fetchTasks()
  },

}

</script>
