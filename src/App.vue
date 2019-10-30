<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>VueMusic</h1>
    <select v-model="selectedCountry">
      <option v-for="(country, index) in countries" :value="country.value" :key="index">{{ country.name }}</option>
    </select>
    <Spinner v-show="loading"/>
    <ul v-show="!loading">
      <Artist
        v-for="artist in artists"
        :key="artist.mbid"
        :artist="artist"
      />
    </ul>
  </div>
</template>

<script>
import getArtists from './api'
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        { value: 'mexico', name: 'Mexico' },
        { value: 'spain', name: 'Espana' },
        { value: 'colombia', name: 'Colombia' },
      ],
      selectedCountry: 'mexico',
      loading: false
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshArtists() {
      const self = this
      this.loading = true
      getArtists(this.selectedCountry)
        .then(function (data) {
          self.artists = data
          self.loading = false
        })
    }
  },
  mounted() {
    this.refreshArtists()
  },
  watch: {
    selectedCountry() {
      this.refreshArtists()
    }
  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }
  
  -webkit-font-smoothing antialiased {
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  
  h1, h2 {
    font-weight: normal;
  }
  
  ul {
    list-style-type: none;
    padding: 0;
  }
  
  li {
    display: inline-block;
    margin: 0 10px;
  }
  
  a {
    color: #42b983;
  }
</style>
