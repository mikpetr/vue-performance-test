<template>
  <div class="hello">
    <h2>{{ msg }}</h2>
    <Calendar/>
  </div>
</template>

<script>

import Calendar from './Calendar';

export default {
  name: 'HelloWorld',
  components: {
    Calendar
  },
  data () {
    return {
      msg: 'Vue Performance Test'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
