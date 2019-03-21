<template lang="pug">
.ranking-item
</template>

<script>
export default {

  props: {
    record: Object
  }

}
</script>

<style lang="sass" scoped>

.ranking-item
  +layout(auto, 100%)

  background-color: #1c3225
  position: relative

  & + &
    margin-top: .4rem

</style>
