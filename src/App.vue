<template lang="pug">
  #app
    .container
      .row.mt-4
        .input-group
          input.form-control(
            type="text",
            placeholder="Buscar canciones...",
            v-model="searchQuery"
          )
          span.input-group-append
            button.btn.btn-info(@click="search") Buscar
          span.input-group-append
            button.btn.btn-danger &times;
      .row.mt-4
        small {{ searchMessage }}
      .row.mt-4
        ul
          li(v-for="t in tracks") {{ t.name }} - {{ t.artists[0].name }}

</template>

<script>
import trackService from './services/track'

export default {
  name: 'app',
  data () {
    return {
      searchQuery: '',
      tracks: []
    }
  },

  computed: {
    searchMessage () {
      return `Encontrados: ${this.tracks.length}`
    }
  },

  methods: {
    search () {
      trackService.search(this.searchQuery)
        .then(res => {
          this.tracks = res.tracks.items
        })
    }
  }
}
</script>

<style lang="scss">

</style>
