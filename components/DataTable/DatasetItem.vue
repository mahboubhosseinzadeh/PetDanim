<template>
  <component :is="tag">
    <template v-for="(rowIndex, i) in dsRows">
      <slot :row="dsData[rowIndex]" :row-index="rowIndex" :index="indexes[i]"></slot>
    </template>

  </component>
</template>

<script>
export default {
  inject: ['rdsData', 'rdsRows', 'rdsFrom', 'rdsTo'],
  props: {
    tag: {
      type: String,
      default: 'div'
    }
  },
  computed: {
    /* Setup reactive injects */
    dsRows() {
      return this.rdsRows()
    },
    dsData() {
      return this.rdsData()
    },
    dsFrom() {
      return this.rdsFrom()
    },
    dsTo() {
      return this.rdsTo()
    },
    indexes() {
      const arr=[]

      for (let i=this.dsFrom;i<this.dsTo;i++) {
        arr.push(i)
      }

      return arr
    }
  }
}
</script>
