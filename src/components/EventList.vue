<template>
  <div id="event-list">
    <h1>Lista de Eventos</h1>

    <!-- CONDITIONAL RENDERING -->
    <template v-if="events.length">
      <div class="event" v-for="(event, index) of events" :key="index">
        <div class="description">
          {{ event.description }}
        </div>
      </div>
    </template>
    <div v-else>
      No hay eventos programados para este día
    </div>

  </div>
</template>

<script>
export default {
  props: {
    events: {
      type: Array,
      default: () => []
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
}

h1 {
  margin: -4px 0 34px 0;
}
</style>
