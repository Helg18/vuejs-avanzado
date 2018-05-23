<template>
  <div id="app">
    <pm-header></pm-header>
    <section class="section">
      <nav class="nav has-shadow">
        <div class="container">
          <div class="field has-addons">
            <div class="control is-expanded">
              <input type="text" class="input is-large" placeholder="Buscar canciones" v-model="searchQuery">
            </div>
            <div class="control">
              <a href="javascript:void(0)" class="button is-info is-large" @click="search"> Buscar</a href="javascript:void(0)">
              <a href="javascript:void(0)" class="button is-danger is-large" @click="clear">&times;</a href="javascript:void(0)">
            </div>
          </div>
        </div>
      </nav>
      <br>
      <div class="container">
        <p>{{ getTotals }}</p><br>
      </div>

      <div v-if="isLoading">
        <pm-loader></pm-loader>
      </div>
      <div class="container" v-else>
        <div class="columns is-multiline">
          <div class="column is-4" v-for="track in tracks">
            <pm-track :track="track" @selectedTrack="setSelectedTrack" :class="{ 'is-selected' : track.id === selectedTrack }"></pm-track>
          </div>
        </div>
      </div>

    </section>
    <pm-footer></pm-footer>
  </div>
</template>

<script>
import trackService from './services/track'
import PmFooter from './components/layouts/Footer.vue'
import PmHeader from './components/layouts/Header.vue'
import PmLoader from './components/layouts/Loader.vue'
import PmTrack from './components/Track.vue'

export default {
  name: 'app',
  components: { PmFooter, PmHeader, PmTrack, PmLoader },
  data () {
    return {
      searchQuery: '',
      tracks: [],
      total: 0,
      isLoading: false,
      selectedTrack: ''
    }
  },
  computed: {
    getTotals () {
      return `Encontrados ${this.total} elementos`
    }
  },
  methods: {
    search () {
      if (this.searchQuery === '') { return }
      this.isLoading = true
      trackService.search(this.searchQuery)
        .then(res => {
          this.total = res.tracks.total
          this.tracks = res.tracks.items
          this.isLoading = false
        })
    },
    clear () {
      this.searchQuery = ''
      this.tracks = []
      this.total = 0
      this.isLoading = false
    },
    setSelectedTrack (id) {
      this.selectedTrack = id
    }
  }
}
</script>

<style lang="scss">
@import "./scss/main.scss";

.margin10 {
  margin: 10px;
}

.is-selected {
  border: 3px #23d160 solid;
}
</style>
