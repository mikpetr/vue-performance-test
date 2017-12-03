<template>
  <div class="calendar">
    <button class="btn" v-if="!isLoaded" v-on:click="load">Load</button>
    <button class="btn" v-if="isLoaded" v-on:click="searchAll">Search all month</button>
    <table v-if="isLoaded">
      <tr>
        <th v-for="(day, key, index) in days" :key="index" class="day-header" @click="dayHeaderClicked(day)">
          {{day}}
        </th>
      </tr>
      <tr v-for="(hour, key, index) in hours" :key="index">
        <td v-for="(day, key, index) in days" :key="index" class="hour-cell">
          <CalendarCell v-bind:hour="hour" v-bind:day="day"/>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
import _ from 'lodash';
import CalendarCell from './CalendarCell';
import service from '../service';

export default {
  name: 'Calendar',
  components: {
    CalendarCell
  },
  data() {
    return {
      hours: _.range(24),
      days: _.range(1, 32).map((day) => ("Oct " + day)),
      isLoaded: false
    }
  },
  methods: {
    load() {
      this.isLoaded = true;
    },
    searchAll() {
      service.searchAllCells();
    },
    dayHeaderClicked() {
      alert('dayHeaderClicked()');
    }
  }
}
</script>

<style scoped>
table {
  border-right: 2px solid gray;
  border-spacing: 0;
  border-collapse: collapse;
}
.day-header {
  border: 1px solid gray;
  white-space: nowrap
}
.day-header:hover {
  cursor: pointer;
}
.hour-cell:hover {
  background-color: #559 !important;
  color: white;
}
.hour-cell {
  width: 120px;
  text-align: center;
  border-left: 1px solid gray;
  border-bottom: 1px solid #eee;
  cursor: pointer;
  height: 30px;
  padding: 0;
}
.hour-cell > div {
  height: 100%;
}
.hour-cell .time {
  padding-top: 10px; /* poor man's vertical centering */
}
.hour-cell .searching {
  color: blue;
  font-size: 12px;
  padding-top: 12px; /* poor man's vertical centering */
}
.hour-cell .good-results {
  color: #090;
  background: #efffef;
}
.hour-cell .weak-results {
  color: orange;
  background: #ffffef;
}
.hour-cell .bad-results {
  color: red;
  background: #ffefef;
}
</style>
