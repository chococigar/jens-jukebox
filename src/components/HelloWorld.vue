<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      Select your mood. Jen will personally recommend you a song.
    </p>
    <model-select :options="options"
                    v-model="item"
                    placeholder="select item"
                    v-on:input="loadMusic">
    </model-select>
    <p> You said : {{ this.item.text }} </p>
    
    <h3>Jen suggests : </h3>
    <youtube :video-id="videoId" :player-vars=" {  autoplay: 1  } " @ready="ready" @playing="playing"></youtube>

  </div>
</template>

<script>
  import {  ModelSelect  } from 'vue-search-select'

  export default {
    name: 'HelloWorld',
    props: {
      msg: String
    },
    data () {
      return {
        options: [
          {  value: '1', text: 'abb' + ' - ' + '1'  },
          {  value: '2', text: 'abc' + ' - ' + '1'  },
          {  value: '3', text: 'ade' + ' - ' + '1'  },
          {  value: '4', text: 'f' + ' - ' + '1'  }
        ],
        item: {
          value: '',
          text: '',
        },
        videoId: 'a7kT52xL-7g'
      }
    },
    methods: {
      reset () {
        this.item = {}
      },
      selectFromParentComponent1 () {
        this.item = this.options[0]
      },
      loadMusic: function (){
        //console.log("this is loading music")

      },
      method (url) {
        this.videoId = this.$youtube.getIdFromURL(url)
        this.startTime = this.$youtube.getTimeFromURL(url)
      },
      ready (event) {
        this.player = event.target
      },
      playing (event) {
        // playing a video,
      }, 
      change () {
        this.videoId = 'another video id'
      },
      stop () {
        this.player.stopVideo()
      },
      pause () {
        this.player.pauseVideo()
      }
    },
    components: {
      ModelSelect
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
