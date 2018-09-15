<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h2 PlatziMusic
    select(v-model="selectedCountry")
      Option(v-for="country in countries" v-bind:value="country.value") {{country.name}}
    Spinner(v-show="loading")
    ul
      artist(v-for="artist in artits"
       v-bind:artist="artist" v-bind:key="artist.mbid")

</template>

<script>
import Artist from './Components/Artist.vue'
import getArtists from './Api'
import Spinner from './Components/spinner.vue'

export default {
  name: 'app',
  data () {
    return {
      artits: [],
      countries: [
        {name: "Argentina" ,value:"Argentina" },
        {name: "Colombia" ,value:"Colombia" },
        {name: "España" ,value:"Spain" }
      ],
      selectedCountry:"Colombia",
      loading: true,
    }
  },
  components:{
    Artist : Artist,
    Spinner : Spinner
  },
  methods:{
    refreshArtists(){
      const self=this
      this.loading=true
      getArtists(this.selectedCountry)
        .then(function(yucamodrich){
          self.loading=false
          self.artits=yucamodrich

        })

    }

  },
  mounted(){
    this.refreshArtists();

  },
  watch: {
    selectedCountry(){
        this.refreshArtists();
    }
  }
}
</script>

<style lang="stylus">
#app
    font-family 'Avenir', Helvetica, Arial, sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
    color green
    margin-top 60px

h1, h2
    font-weight normal

ul
    list-style-type none
    padding 0

li
    display inline-block
    margin 0 10px

a
    color #42b983
</style>
