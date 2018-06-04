<template lang="pug">
  #app
    vm-header
    .container.py-4
      .row.mb-4
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
      .row.mb-4
        small {{ searchMessage }}
      .row.mb-4
        ul
          li(v-for="t in tracks") {{ t.name }} - {{ t.artists[0].name }}

    vm-footer

</template>

<script>
import trackService from './services/track'
import VmFooter from './components/layout/Footer.vue'
import VmHeader from './components/layout/Header.vue'

export default {
  name: 'app',
  components: { VmFooter, VmHeader },
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
    html, body {
        height: 100%;
        margin: 0;
    }

    html, body, *, *:before, *:after {
        -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        box-sizing: border-box;
    }

    body {
        padding-bottom: 50px;
    }
</style>
