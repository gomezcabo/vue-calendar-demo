<template>
  <div id="home">
    <div id="calendar-form">
      <h1>Calendario</h1>

        <!-- COMPONENTE CALENDARIO -->
        <calendar :tasks="tasks" @selectedDay="selectedDay = $event" />

        <!-- TASK FORM COMPONENT -->
        <task-form @taskCreated="addTask" />

    </div>
    <div id="tasks">

      <!-- TASK LIST COMPONENT -->
      <task-list :tasks="tasksSelected" @deletedTask="deleteTask" />

    </div>
  </div>
</template>

<script>
import moment from 'moment'
import Calendar from '@/components/Calendar'
import TaskList from '@/components/TaskList'
import TaskForm from '@/components/TaskForm'

let currentId = 0
const initialTasks = [
  { id: currentId++, day: '20181101', description: 'Entregar documentación a Batman' },
  { id: currentId++, day: '20181107', description: 'Tarea 1' },
  { id: currentId++, day: '20181107', description: 'Tarea 2' },
  { id: currentId++, day: '20181107', description: 'Tarea 3' },
  { id: currentId++, day: '20181110', description: 'JSDay - Día 1' },
  { id: currentId++, day: '20181111', description: 'JSDay - Día 2' }
]

const today = moment().format('YYYYMMDD')

export default {
  name: 'App',
  data () {
    return {
      tasks: initialTasks,
      selectedDay: today
    }
  },
  computed: {
    tasksSelected () {
      return this.tasks.filter(e => e.day === this.selectedDay)
    }
  },
  methods: {
    addTask (description) {
      this.tasks.push({
        id: currentId++,
        day: this.selectedDay,
        description
      })
    },
    deleteTask (taskId) {
      this.tasks = this.tasks.filter(task => task.id !== taskId)
    }
  },
  components: {
    Calendar,
    TaskList,
    TaskForm
  }
}
</script>

<style lang="scss">
$page-padding: 10px;

#home {
  display: flex;
  padding: $page-padding;
  height: calc(100vh - #{2 * $page-padding});

  #calendar-form {
    flex: 1;
    margin: 20px;

    > *:first-of-type {
      margin-bottom: 30px;
    }
  }

  #tasks {
    display: block;
    flex: 1;
    margin: 20px;
  }

  h1 {
    margin: 0 0 30px 0;
  }
}

html {
  background-color: #555;
}

body {
  margin: 0 auto;
  padding: 0;
  max-width: 1200px;
  background: white;
  box-shadow: 0px 2px 28px -8px rgba(0,0,0,0.95);
}

body, input, button {
  font-family: 'Roboto Mono', 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

h1 {
  color: #de3800;
}
</style>
