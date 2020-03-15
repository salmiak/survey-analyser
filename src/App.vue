<template>
  <div id="app">
    <DataCollector @data-loaded="surveyData = $event" />
    <div v-if="surveyData">
      <div v-for="(key,indx) in surveyData.keys" :key="key">
        <h2>{{key}}</h2>
        <histogram :data="surveyData.rows" :filter="filter" :index="indx" />
        <input v-model="filter[indx]" />
      </div>
    </div>
  </div>
</template>

<script>
import DataCollector from './components/DataCollector.vue'
import Histogram from './components/Histogram.vue'

export default {
  name: 'App',
  components: {
    DataCollector,
    Histogram
  },
  data() {
    return {
      surveyData: undefined,
      filter: {}
    }
  },
  methods: {
    log(val) {
      console.log(val) // eslint-disable-line no-console
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
