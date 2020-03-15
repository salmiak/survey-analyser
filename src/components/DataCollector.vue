<template lang="html">
  <div class="dataCollector">
    <textarea v-model="dataSource" placeholder="Data goes here" :style="{'height':dataSource?'30px':'300px'}"></textarea>
  </div>
</template>

<script>
import _ from 'lodash'

export default {
  name: 'DataCollector',
  data() {
    return {
      dataSource: undefined
    }
  },
  computed: {
    parsedData() {
      if (!this.dataSource) {
        return []
      }
      var lines = _.trim(this.dataSource).split('\n');
      var keys = lines.shift().split('\t')
      var rows = lines.map((line) => {
        return line.split('\t')
      })
      return {
        keys,
        rows
      }
    }
  },
  watch: {
    parsedData(val) {
      this.$emit('data-loaded',val)
    }
  }
}
</script>

<style lang="css" scoped>
textarea {
  width: 100%;
  border: 1px solid #DDD;
  border-radius: 6px;
  transition: all 0.5s;
  outline: none;
}
textarea:focus {
  height: 300px !important;
  border: 1px solid #AAA;
}
</style>
