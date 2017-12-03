<template>
  <div v-bind:class="{
    goodresults: status.searchResults.options > 3,
    weakresults: status.searchResults.options >= 1 && status.searchResults.options <= 3,
    badresults: status.searchResults.options == 0,
    searching: status.isSearching
  }">
    <div v-if="showSpinner()">
      ...
    </div>
    <div v-if="showTime()" v-on:click="cellClicked" class="time">
      {{hour}}:00
    </div>
    <div v-if="showSearchResults()">
      <div>{{status.searchResults.options}}</div>
      <div class="result-label">results</div>
    </div>
  </div>
</template>

<script>
function randomMilliseconds () {
  return Math.floor(Math.random() * 500);
}

import service from '../service';

export default {
  name: 'CalendarCell',
  props: ['day', 'hour'],
  data() {
    service.addCell(this);

    return {
      status: {
        isSearching: false,
        searchResults: {
          options: null
        }
      }
    }
  },
  methods: {
    cellClicked() {
      let alreadySearching = this.status.isSearching;

      this.status.searchResults.options = null;
      this.status.isSearching = !alreadySearching;

      if (!alreadySearching) {
        // Simulate an AJAX request:
        this.status.isSearching = true;

        setTimeout(() => {
          this.status.isSearching = false;
          this.status.searchResults.options = Math.floor(Math.random() * 5);
        }, randomMilliseconds());
      }
    },
    showSpinner() {
      return this.status.isSearching;
    },
    hideSpinner() {
      return !this.status.isSearching;
    },
    showTime() {
      return !this.status.isSearching && this.status.searchResults.options === null;
    },
    showSearchResults() {
      return !this.status.isSearching && this.status.searchResults.options !== null;
    }
  }
};
</script>

<style scoped>
.searching {
  color: blue;
  font-size: 10px;
  padding-top: 6px; /* poor man's vertical centering */
}
.goodresults {
  color: #090;
  background: #efffef;
}
.result-label {
  font-size: 8px;
}
.weakresults {
  color: orange;
  background: #ffffef;
}
.badresults {
  color: red;
  background: #ffefef;
}
:hover {
  background-color: #559 !important;
  color: white;
}
</style>
