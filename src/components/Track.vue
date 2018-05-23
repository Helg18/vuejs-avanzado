<template>
  <div class="card" @click="selected">
    <div class="card-image">
      <figure class="image 1by1">
        <img v-bind:src="track.album.images[1].url" v-bind:alt="track.name" width="60px" height="60px">
      </figure>
    </div>

    <div class="card-content">
      <div class="media">
        <div class="media-left">
          <figure class="image is-48x48">
            <img v-bind:src="track.album.images[2].url" v-bind:alt="track.name">
          </figure>
        </div>

        <div class="media-content">
          <p class="title is-6">{{ track.name }}</p>
          <p class="subtitle is-6">{{ track.artists[0].name }}</p>
          <p class="small">Preview 30 segundos
            <audio controls>
              <source v-bind:src="track.preview_url" type="audio/mpeg">
              Your browser does not support the audio tag.
            </audio>
          </p>
          <small>Duracion: {{ track.duration_ms }}</small>
        </div>
      </div>

      <div class="content">.
        <br>
        <time :datetime="track.album.release_date">Release date {{ track.album.release_date }}</time>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      track: { type: Object, required: true }
    },
    methods: {
      selected () {
        this.$emit('selectedTrack', this.track.id)
      }
    }
  }
</script>