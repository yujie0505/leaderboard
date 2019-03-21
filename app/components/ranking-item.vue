<template lang="pug">
.ranking-item
  img(:src="record.avatar || require('../assets/icon.png')")
  .meta
    .name {{ record.name }}
    .record
      div(v-for="type in types" :class="type")
        img(:src="require(`../assets/tree_${type}.png`)")
        span {{ record[`${type}_count`] }}
      .time {{ record.total_minutes }} 分鐘
</template>

<script>
export default {

  data () {
    return {
      types: ['health', 'dead']
    }
  },

  props: {
    record: Object
  }

}
</script>

<style lang="sass" scoped>

.ranking-item
  +layout(4rem, 100%, .25rem)

  background-color: #1c3225
  box-sizing: border-box
  color: #d1ccbb
  display: inline-block
  position: relative

  & + &
    margin-top: .4rem

  > img
    border-radius: 50%
    float: left
    height: 100%
    margin-right: 1rem

  .meta
    display: flex
    flex-direction: column
    font-size: 1.1rem
    height: 100%

    > div
      align-items: center
      display: flex
      height: 50%

  .record

    > div
      display: flex
      flex: 1

      &.time
        justify-content: flex-end
        margin-right: .3rem

      > img
        +layout(1.5rem, 1.5rem, 0, 0 .5rem 0 0)

</style>
