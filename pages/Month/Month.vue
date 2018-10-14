<template>
  <div>
   <!-- <SelectIcons></SelectIcons> -->
    <MonthHeader
      :current_month="current_month"
    >
    </MonthHeader>

    <v-layout row>
      <v-flex xs2 v-for="i in WEEK" :key="i">
        <v-card color="blue lighten-2" text-darken-1>
          <v-card-text class="px-0 text-xs-center">{{week_days[i-1]}}</v-card-text>
        </v-card>
      </v-flex>
    </v-layout>

    <div v-for="i in week_num_by_month" :key="i">
      <v-layout row>
        <v-flex xs2 row v-for="j in WEEK" :key="j">
          <CalenderDate
            :dateState="computeDateType((i-1)*WEEK + j - first_day,j == WEEK,j == 1)"
          ></CalenderDate>
        </v-flex>
      </v-layout>
    </div>

    <!--
<v-dialog
  persistent
  width="800"
>
  <v-card>
    <v-card-title>
      Dialog
    </v-card-title>
    <v-card-actions>
      <v-btn color="primary" flat @click="setDetailDialog(false)">Close</v-btn>
    </v-card-actions>
  </v-card>
</v-dialog>
-->
  </div>

</template>

<script>

import CalenderDate from './CalenderDate'
import MonthHeader from './MonthHeader'
// import {mapGetters, mapMutations} from 'vuex'
import SelectIcons from './SelectIcons'

export default {
  name: 'Calender',
  components: {
    SelectIcons,
    MonthHeader,
    CalenderDate
  },
  data: () => {
    return {
      num_of_date: 0,
      week_days: ['日', '月', '火', '水', '木', '金', '土'],
      WEEK: 7,
      week_num_by_month: 0,
      last_date_by_current_month: 0,
      first_day: 0,
      last_date_by_prev_month: 0,
      last_day: 0,
      current_month: 0,
      current_date: 0,
      is_active: false

    }
  },
  /*
  computed: {
    ...mapGetters('date', ['getDetailDialog']),
    testa: function (data) {
      console.log(data)
      return data.item
    }
  }, */
  mounted () {
    let now = new Date()
    let year = now.getFullYear()
    this.current_month = now.getMonth() + 1
    this.current_date = now.getDate()
    this.last_date_by_current_month = this.getDaysByMonth(year, this.current_month)
    this.last_date_by_prev_month = this.getDaysByMonth(year, this.current_month - 1)
    this.first_day = this.getFirstDay(year, this.current_month - 1)
    this.last_day = this.getLastDay(year, this.current_month - 1, this.last_date_by_current_month)
    this.week_num_by_month = Math.ceil(this.last_date_by_current_month / 7)
  },
  methods: {
    // ...mapMutations('date', ['setDetailDialog']),

    getDaysByMonth: function (year, month) {
      return new Date(year, month, 0).getDate()
    },
    getFirstDay: function (year, month) {
      return new Date(year, month, 1).getDay()
    },
    getLastDay: function (year, month, lastDay) {
      return new Date(year, month, lastDay).getDay()
    },
    computeDateType: function (targetDate, isSaturday, isSunday) {
      let dateState = {
        is_work: false,
        date: targetDate,
        isSaturday,
        isSunday,
        dateType: ''
      }
      if (targetDate < 1 || targetDate > this.last_date_by_current_month) {
        if (targetDate < 1) {
          dateState.date = this.last_date_by_prev_month + targetDate
        } else {
          dateState.date = targetDate - this.last_date_by_current_month
        }
        dateState.isSunday = false
        dateState.isSaturday = false
        dateState.dateType = 'exclude_date'
      } else if (this.current_date < targetDate) {
        dateState.dateType = 'future_date'
      } else if (this.current_date === targetDate) {
        dateState.dateType = 'current_date'
      } else {
        dateState.dateType = 'past_date'
      }
      if (!isSaturday && !isSunday) {
        dateState.is_work = true
      }

      return dateState
    }
  }
}
</script>

<style scoped>

</style>
