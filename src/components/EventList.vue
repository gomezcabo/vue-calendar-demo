<template>
  <div id="event-list">
    <h1>Eventos {{ day }}</h1>

    <!-- CONDITIONAL RENDERING -->
    <div class="empty" v-if="!events.length">
      No hay eventos programados para este día
    </div>
    <template v-else>
      <div class="event" v-for="(event, index) of events" :key="index">
        <div class="description">
          {{ event.description }}
        </div>
      </div>
    </template>

  </div>
</template>

<script>
import moment from 'moment'

export default {
  props: {
    events: {
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
#event-list {
  .event {
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
