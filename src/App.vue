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
                <img src="https://picsum.photos/100/100/?random" alt="">
              </figure>
              <div class="column">
                <p class="title">{{track.name}}</p>
                <p class="subtitle">{{track.artist}}</p>
              </div>
            </article>
          </div>
        </div>
      </div>

    </section>
  </div>
</template>

<script>
const tracks = [
  { name: 'A donde vayas', artist: 'Alex Bueno' },
  { name: 'A donde vayas', artist: 'Alex Bueno' },
  { name: 'A donde vayas', artist: 'Alex Bueno' },
  { name: 'A donde vayas', artist: 'Alex Bueno' },
  { name: 'Hard to say Im sorry', artist: 'Chicago' },
  { name: 'Hard to say Im sorry', artist: 'Chicago' },
  { name: 'Hard to say Im sorry', artist: 'Chicago' },
  { name: 'Hard to say Im sorry', artist: 'Chicago' },
  { name: 'Its must been love', artist: 'Roxette' }
]

export default {
  name: 'app',
  data () {
    return {
      searchQuery: '',
      tracks: []
    }
  },
  computed: {
    getTotals () {
      return `Encontrados ${this.tracks.length} elementos`
    }
  },
  methods: {
    search () {
      this.tracks = tracks
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
