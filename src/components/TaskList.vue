<template>
  <div id="task-list">
    <h1>Tareas</h1>

    <!-- CONDITIONAL RENDERING -->
    <div class="empty" v-if="!tasks.length">
      No hay tareas el {{ day }}
    </div>
    <template v-else>
      <div class="task" v-for="(task, index) of tasks" :key="index">
        <div class="description">
          {{ task.description }}
        </div>
      </div>
    </template>

  </div>
</template>

<script>
import moment from 'moment'

export default {
  props: {
    tasks: {
      type: Array,
      default: () => []
    },
    selectedDay: {
      type: String,
      default: ''
    }
  },
  computed: {
    day () {
      return moment(this.selectedDay).format('DD-MM-YYYY')
    }
  }
}
</script>

<style lang="scss" scoped>
#task-list {
  .task {
    padding: 15px 20px;
    border: 1px solid #ddd;
    margin: 8px 0;
    display: flex;
    justify-content: space-between;

    .delete {
      cursor: pointer;
      color: darkred;
      font-weight: bold;
    }
  }

  .empty {
    padding-top: 20px;
  }
}

h1 {
  margin: -4px 0 34px 0;
}
</style>
