<template lang="pug">
  el-table(:data="data" stripe)
    el-table-column(
      v-for="(item, index) in config"
      :key="index"
      :label="item.label")
      template(slot-scope="scope")
        span(v-html="realValue.bind(this, scope.row, item)()")
    el-table-column(
      label="操作"
      v-if="operations.length")
      template(slot-scope="scope")
        el-button(
          v-for="(btn, index) in operations",
          :key="index"
          :type="btn.type"
          @click="btn.action.bind(this, scope)()"
        ) {{btn.label}}
</template>
<script>
export default {
  name: 'SmartTable',
  components: {},
  props: {
    data: {
      type: Array,
      required: true
    },
    config: {
      type: Array,
      required: true
    },
    operations: {
      type: Array,
      required: false,
      default () { return [] }
    }
  },
  data () {
    return {
    }
  },
  computed: {},
  created () {},
  mounted () {},
  methods: {
    realValue (row, item) {
      let value = row[item.prop]
      if (typeof item.formatter === 'function') {
        return item.formatter(row, item)
      } else {
        return value
      }
    }
  }
}
</script>
<style lang="stylus" rel="stylesheet/stylus" scoped>
</style>
