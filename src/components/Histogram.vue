<template lang="html">
  <div class="histogram">
    <apexchart width="100%" height="300px" type="bar" :options="chartOptions" :series="series"></apexchart>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  name:"Histogram",
  props: [
    'data',
    'index',
    'filter'
  ],
  data() {
    return {
    }
  },
  computed: {
    filteredData() {
      const _this = this
      return _.filter(this.data, function(row) {
        const logic = _.keys(_this.filter).map((key) => {
          return row[key] == _this.filter[key] || _this.filter[key] === ""
        });
        return logic.indexOf(false) === -1
      })
    },
    countedData() {
      return _.countBy(_.unzip(this.data)[this.index], (v) => v)
    },
    countedDataFiltered() {
      return _.countBy(_.unzip(this.filteredData)[this.index], (v) => v)
    },
    filteredSerie() {
      return _.keys(this.countedData).map((key) => {
        return this.countedDataFiltered[key] || 0
      })
    },
    series() {
      return [{
        name: 'all',
        data: _.values(this.countedData)
      },{
        name: 'filtered',
        data: this.filteredSerie
      },]
    },
    chartOptions() {
      return {
        xaxis: {
          categories: _.keys(this.countedData)
        }
      }
    }
  }
}
</script>

<style lang="css" scoped>
</style>
