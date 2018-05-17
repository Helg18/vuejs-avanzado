<template>
  <div id="app">
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
        <p>{{ getTotals }}</p>
        <div class="tile is-ancestor" v-for="track in tracks">
          <div class="tile is-parent is-inline-block">
            <article class="tile is-child box columns">
              <figure>
                <img v-bind:src="track.album.images[1].url" v-bind:alt="track.name" height="180px" width="180px">
              </figure>
              <div class="column">
                <p class="title">{{track.name}}</p>
                <p class="subtitle">{{track.artists[0].name}}</p>
                <p class="small">Preview
                  <audio controls>
                    <source v-bind:src="track.preview_url" type="audio/mpeg">
                    Your browser does not support the audio tag.
                  </audio>
                </p><br>
              </div>
            </article>
          </div>
        </div>
      </div>

    </section>
  </div>
</template>

<script>
import trackService from './services/track'

export default {
  name: 'app',
  data () {
    return {
      searchQuery: '',
      tracks: [],
      total: 0
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

      trackService.search(this.searchQuery)
        .then(res => {
          this.total = res.tracks.total
          this.tracks = res.tracks.items
        })
    },
    clear () {
      this.searchQuery = ''
    }
  }
}
</script>

<style lang="scss">
@import "./scss/main.scss";

.margin10 {
  margin: 10px;
}
</style>
