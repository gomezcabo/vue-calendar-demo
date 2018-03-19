<template>
  <div class="calendar">
    <!-- <div class="data">
      Current day: {{ currentDate }}<br>
      Month: {{ month }}<br>
      Year: {{ year }}<br>
      Days in Month: {{ daysInMonth }}<br>
      First Day of Month: {{ lastDayOfMonth }}<br>
    </div> -->

    <div class="actions">
      <a @click="prevMonth">⇠</a>
      <div class="month">{{ monthName }} {{ year }}</div>
      <a @click="nextMonth">⇢</a>
    </div>

    <div v-for="day of weekDays" :key="'header' + day" class="day header">
      {{ day }}
    </div>

    <template v-if="extraDaysBefore > 0">
      <div v-for="day of extraDaysBefore" :key="'pre' + day" class="day empty">
        <!-- empty -->
      </div>
    </template>
    <div v-for="day of daysInMonth" :key="day" class="day">
      {{ day }}
    </div>

    <template v-if="extraDaysAfter > 0">
      <div v-for="day of extraDaysAfter" :key="'post' + day" class="day empty">
        <!-- empty -->
      </div>
    </template>
  </div>
</template>

<script>
import moment from 'moment'

const weekDays = ['LUN', 'MAR', 'MIE', 'JUE', 'VIE', 'SAB', 'DOM']
const monthNames = [
  'ENERO',
  'FEBRERO',
  'MARZO',
  'ABRIL',
  'MAYO',
  'JUNIO',
  'JULIO',
  'AGOSTO',
  'SEPTIEMBRE',
  'OCTUBRE',
  'NOVIEMBRE',
  'DICIEMBRE'
]

const today = moment()

export default {
  data () {
    return {
      weekDays,
      today,
      month: today.month(),
      year: today.year()
    }
  },
  computed: {
    currentDate () {
      return moment().year(this.year).month(this.month)
    },
    daysInMonth () {
      return this.currentDate.daysInMonth()
    },
    firstDayOfMonth () {
      return this.currentDate.startOf('month')
    },
    lastDayOfMonth () {
      return this.currentDate.endOf('month')
    },
    extraDaysBefore () {
      return this.firstDayOfMonth.day() - 1
    },
    extraDaysAfter () {
      return 7 - this.lastDayOfMonth.day()
    },
    monthName () {
      return monthNames[this.month]
    }
  },
  methods: {
    prevMonth () {
      if (this.month === 0) {
        this.month = 11
        this.year--
      } else {
        this.month--
      }
    },
    nextMonth () {
      if (this.month === 11) {
        this.month = 0
        this.year++
      } else {
        this.month++
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.data {
  width: 100%;
  display: block;
}
.calendar {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  border: 1px solid #eee;

  .actions {
    display: flex;
    width: 100%;
    justify-content: space-between;
    align-items: center;
    padding: 2px;
    font-weight: bold;

    .month {
      color: darkolivegreen;
      font-size: 26px;
    }

    a {
      padding: 4px 12px;
      cursor: pointer;
      background: #ddd;
    }
  }

  .day {
    width: calc(100% * (1/7) - 24px);
    padding: 10px;
    margin: 2px;
    position: relative;
    display: inline-block;
    background-color: #eee;
    text-align: center;
    color: darkslategray;

    &.empty {
      background: #fafafa;
    }

    &.header {
      background: transparent;
      font-weight: bold;
    }

    &:not(.empty):hover {
      cursor: pointer;
      background-color: #ddd;
    }
  }
}
</style>
