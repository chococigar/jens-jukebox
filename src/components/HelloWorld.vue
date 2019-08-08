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
    <div v-if="item.value">
      <h3>Jen suggests : </h3>

      <youtube :video-id="videoId" :player-vars=" {  autoplay: 1  } " @ready="ready" @playing="playing"></youtube>
    </div>

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
          {  value: 'workout', text: 'workout'  },
          {  value: 'sad', text: 'sad'  },
          {  value: 'lit', text: 'lit'  },
          {  value: 'solo', text: 'solo'  },
          {  value: 'hopeful', text: 'hopeful'  },
          {  value: 'powerwoman', text: 'powerwoman'  },
          {  value: 'happy', text: 'happy'  },
          {  value: 'studying', text: 'studying'  },
          {  value: 'angry', text: 'angry'  },
          {  value: 'nervous', text: 'nervous'  },
          {  value: 'lonely', text: 'lonely'  }
        ],
        item: {
          value: '',
          text: '',
        },
        videoId: 'a7kT52xL-7g' // fallback IWIMME
      }
    },
    created() {
      this.powerwoman = [
        {  name: "OhNo", videoId : "Cr-SqRWImmI"  },
        {  name: "Primadonna", videoId : "Gj5L9SYhoSE"  },
        {  name: "HowToBeAHeartBreaker", videoId : "vKNcuTWzTVw"  },
        {  name: "PopStars", videoId : "UOxkGD8qRB4"  },
        {  name: "GonnaGetOverYou", videoId : "OUe3oVlxLSA"  },
      ],
      this.happy = [
        {  name: "AltogetherAlone", videoId : "S9ZocwLckQw"  },
        {  name: "ThousandMiles", videoId : "Cwkej79U3ek"  },
      ]
    },
    methods: {
      reset () {
        this.item = {}
      },
      selectFromParentComponent1 () {
        this.item = this.options[0]
      },
      loadMusic (){
        this.pickMusic(this.item.value)
      },
      pickMusic (mood) {
        console.log(mood);
        console.log(this[mood]);
        var randomSongInd = Math.floor(Math.random() * this[mood].length);
        this.videoId = this[mood][randomSongInd].videoId;
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
