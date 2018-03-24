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

const today = moment().format('YYYYMMDD')

export default {
  name: 'Home',
  data () {
    return {
      // INITIAL TASKS
      tasks: [
        { id: 1, day: '20180328', description: 'CanariasJS meetup!!' },
        { id: 2, day: '20180329', description: 'Vacaciones' },
        { id: 3, day: '20180401', description: 'Uno de abril' },
        { id: 4, day: '20180423', description: 'Día del libro' }
      ],
      currentId: 5,
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
        id: this.currentId++,
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

<style lang="scss" scoped>
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
    margin: 0 0 20px 0;
  }
}
</style>
