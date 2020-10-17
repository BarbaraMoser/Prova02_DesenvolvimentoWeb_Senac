<template>
  <div id="dashboards">
    <h1>Painel dos Projetos</h1>
    <calculos :areas='areas'></calculos>
  </div>
</template>


<script>
import axios from 'axios'
import Calculos from '../components/Calculos'

export default {
  components: {
    Calculos,
  },

  data() {
    return {
      areas: [],
    }
  },
  mounted() {
      axios.get('https://projeto-prova.herokuapp.com/projeto').then(response => {
          this.areas = response.data
      })
  },
  methods: {

  }
}
</script>

<style>


</style>
