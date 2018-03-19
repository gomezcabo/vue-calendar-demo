<template>
  <div class="calendar">

    <!-- PREV/NEXT actions & HEADER -->
    <div class="actions">
      <a @click="prevMonth">⇠</a>
      <div class="month">{{ monthName }} {{ year }}</div>
      <a @click="nextMonth">⇢</a>
    </div>

    <!-- DAY NAMES HEADER -->
    <div v-for="day of weekDays" :key="'header' + day" class="day header">
      {{ day }}
    </div>

    <!-- EXTRA DAYS BEFORE -->
    <template v-if="extraDaysBefore > 0">
      <div v-for="day of extraDaysBefore" :key="'pre' + day" class="day empty"><!-- empty --></div>
    </template>

    <!-- MONTH DAYS -->
    <div
      v-for="day of daysInMonth"
      :key="day"
      class="day"
      :class="{ 'selected': isSelectedDay(day), 'has-events': dayHasEvents(day) }"
      @click="selectDay(day)"
    >
      {{ day }}
    </div>

  </div>
</template>

<script>
import moment from 'moment'

const today = moment()
const weekDays = ['LUN', 'MAR', 'MIE', 'JUE', 'VIE', 'SAB', 'DOM']
const monthNames = ['ENE', 'FEB', 'MAR', 'ABR', 'MAY', 'JUN', 'JUL', 'AGO', 'SEP', 'OCT', 'NOV', 'DIC']

export default {
  props: {
    events: {
      type: Array,
      default: () => []
    }
  },
  data () {
    return {
      weekDays,
      today,
      selectedDay: today,
      month: today.month(),
      year: today.year()
    }
  },
  computed: {
    // CURRENT MONTH
    currentMonth () {
      return moment().year(this.year).month(this.month)
    },
    // NUMBER OF DAYS IN MONTH
    daysInMonth () {
      return this.currentMonth.daysInMonth()
    },
    // EXTRA DAYS
    extraDaysBefore () {
      return this.currentMonth.startOf('month').day() - 1
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
    },
    isSelectedDay (day) {
      const currentDay = moment().year(this.year).month(this.month).date(day).format('YYYYMMDD')
      return currentDay === this.selectedDay.format('YYYYMMDD')
    },
    dayHasEvents (day) {
      const currentDay = moment().year(this.year).month(this.month).date(day).format('YYYYMMDD')
      return this.events.filter(e => e.day === currentDay).length > 0
    },
    selectDay (day) {
      this.selectedDay = moment().year(this.year).month(this.month).date(day)
      this.$emit('selectedDay', this.selectedDay.format('YYYYMMDD'))
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
    margin-bottom: 10px;
    font-weight: bold;

    .month {
      color: darkolivegreen;
      font-size: 22px;
    }

    a {
      margin: 10px 20px;
      padding: 10px 20px;
      border-radius: 4px;
      cursor: pointer;

      &:hover {
        background-color: #eeeeee;
      }
    }
  }

  .day {
    width: calc(100% * (1/7) - 24px);
    padding: 10px 6px;
    border-radius: 3px;
    margin: 6px 6px;
    position: relative;
    display: inline-block;

    text-align: center;
    color: darkslategray;

    &.empty {
      background: white;
    }

    &.header {
      background: transparent;
      font-weight: bold;
    }

    &.has-events {
      font-weight: bold;
      color: darkred;
      background-color: rgba(lightcoral, 0.5);

      &:before { content: '-' }
      &:after  { content: '-' }
    }

    &.selected {
      background-color: greenyellow;
      cursor: default;
    }

    &:not(.empty):not(.header):not(.selected):hover {
      cursor: pointer;
      background-color: #eeeeee;
    }
  }
}
</style>
