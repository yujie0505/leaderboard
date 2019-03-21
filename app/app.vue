<template lang="pug">
#v-app
  #nav #[h1 森林排行榜]
  #ranking-list
    v-ranking-item(v-for="(record, idx) in ranking" :key="idx" :record="record")
</template>

<script>
import axios from 'axios'

export default {

  components: {
    'v-ranking-item': require('./components/ranking-item.vue').default
  },

  created () {
    this.loadRanking()
  },

  data () {
    return {
      ranking: []
    }
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
    font-weight: lighter
    margin: 0

</style>
