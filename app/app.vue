<template lang="pug">
#v-app
  #nav #[h1 森林排行榜]
  #ranking-list
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

<style lang="sass" scoped>

#v-app
  +layout(100%, 100%)

  background-color: #244334

#nav
  +layout(auto, 100%, .7rem 0)

  background-color: #111d1b
  color: #d1ccbb
  text-align: center

  h1
    margin: 0

</style>
