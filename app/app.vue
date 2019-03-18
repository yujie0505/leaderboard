<template lang="pug">
</template>

<script>
import axios from 'axios'

export default {

  data () {
    return {
      ranking: []
    }
  },

  created () {
    this.loadRanking()
  },

  methods: {

    loadRanking () {
      const vm = this

      axios.get(`https://testsite.staging.seekrtech.com/forest_rankings?n=20&last_pos=${vm.ranking.length}`)
        .then(res => vm.ranking.push(...res.data.ranking))
    }

  }

}
</script>

<style lang="sass">
</style>
