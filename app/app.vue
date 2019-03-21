<template lang="pug">
#v-app
  #nav #[h1 森林排行榜]
  #ranking-list
    v-ranking-item(v-for="(record, idx) in ranking" :key="record.user_id" :ranking="idx + 1" :record="record")
    #loading Loading
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
      loading: false,
      ranking: []
    }
  },

  methods: {

    loadRanking () {
      const vm = this

      return axios.get(`https://testsite.staging.seekrtech.com/forest_rankings?n=20&last_pos=${vm.ranking.length}`)
        .then(res => vm.ranking.push(...res.data.ranking))
    }

  },

  mounted () {
    const vm = this

    document.getElementById('ranking-list').addEventListener('scroll', () => {
      if (vm.loading)
        return

      const bottom = document.getElementById('loading'),
            list = document.getElementById('ranking-list')

      if (list.scrollTop >= list.scrollHeight - list.clientHeight - bottom.clientHeight) {
        vm.loading = true

        vm.loadRanking().then(() => vm.loading = false)
      }
    })
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
    line-height: 1
    margin: 0

#ranking-list
  +layout(calc(100vh - 4.4rem), 100%, 0 .4rem 0 .7rem, .5rem 0)

  box-sizing: border-box
  overflow-y: scroll

  &::-webkit-scrollbar
    background-color: transparent
    width: .3rem

  &::-webkit-scrollbar-thumb
    background-color: #aaa
    border-radius: 1rem

#loading
  color: #d1ccbb
  font-style: italic
  margin: .5rem 0
  text-align: center

  &::after
    animation: loading 2s infinite
    content: ''
    margin-left: .2rem

// loading animation

@keyframes loading
  0%   { content: ''     }
  25%  { content: '.'    }
  50%  { content: '..'   }
  75%  { content: '...'  }
  100% { content: '....' }

</style>
