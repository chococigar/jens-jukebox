<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>Because Jen does it the best.</px>
    <p>
      Select your mood. Jen will personally recommend you a song.
    </p>
    <!--<model-select :options="options"
                    v-model="item"
                    placeholder="select item"
                    v-on:input="loadMusic">
    </model-select>  -->
    <ul>
      <li 
        v-for="emo in emoji" 
        style="font-size:4em; margin:0px"
        v-on:click='pickMusic(emo.value)'>
          {{  emo.disp }}
      </li>
    </ul>
    <div v-if="videoId">
      <h3>Jen suggests {{  this.videoName  }}.</h3>

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
        emoji: [
          {  disp: '🕵️‍♂️', value:'spy'  },
          {  disp: '😢', value:'lonely'  },
          {  disp: '🤪', value:'crazy'  },
          {  disp: '🤬', value:'angry'  },
          {  disp: '🥰', value:'loving'  },
          {  disp: '🏃‍♀️', value:'workout'  },
          {  disp: '🤷‍♂️', value:'whatever'  },
          {  disp: '😌', value:'chill'  },
          {  disp: '👏 ', value:'upbeat'  },
          {  disp: '😰', value:'scared'  },
          {  disp: '👩‍💻', value:'studying'  },
          {  disp: '👊', value:'powerwoman'  },
          {  disp: '🕳', value:'sad'  },
          {  disp: '🍸', value:'french'  }
        ],
        item: {
          value: '',
          text: '',
        },
        videoId: null, // fallback IWIMME
        videoName: null // fallback
      }
    },
    created() {
      this.spy = [
        {  name: 'Dance of the knights', videoId : 'DUmq1cpcglQ'  },
        {  name: 'Piano Concerto no.2 op.18', videoId : 'rEGOihjqO9w'  },
        {  name: 'Katyusha', videoId : '7J__ZdvsZaE'  },
        {  name: 'Piano Concerto no.2 op.18', videoId : 'rEGOihjqO9w'  },
        {  name: 'Waltz No.2', videoId : 'mmCnQDUSO4I'  },
        {  name: 'Genius', videoId : 'HhoATZ1Imtw'  },
      ],
      this.lonely = [
        {  name: 'Everybody\'s changing', videoId : 'Zx4Hjq6KwO0'  },
        {  name: 'You and I', videoId : 'oGEwc4xap0E'  },
        {  name: 'Let you love me', videoId : 'XCQK6LmhYqc'  },
        {  name: 'Daughter', videoId : 'VEpMj-tqixs'  },
        {  name: 'Stay high', videoId : 'oh2LWWORoiM'  },
        {  name: 'Dear old Nicki', videoId : '-NZFsjWHC9I'  },
        {  name: 'Catcher in the Rye', videoId : '4PNNzSNtihI'  },

      ],
      this.crazy = [
        {  name: 'Hallucinating', videoId : 'DzOpGMg8g5M'  },
        {  name: 'I go crazy', videoId : 'evUe46ua8Ao'  }
      ],
      this.angry = [
        {  name: 'Evil deeds', videoId : 'M7LRcDMVMTw'  },
        {  name: 'Bury a friend', videoId : 'HUHC9tYz8ik'  },
        {  name: 'Kamikaze', videoId : 'jQh3YBAVWCE'  },
        {  name: 'Five nights at Freddie\'s', videoId : 'AjIXqh6q6Bg'  },
      ],
      this.loving = [
        {  name: 'Lover Boy', videoId : '8HnLRrQ3RS4'  },
        {  name: 'Altogether Alone', videoId : 'S9ZocwLckQw'  },
        {  name: 'Thousand Miles', videoId : 'Cwkej79U3ek'   },
        {  name: 'Back to you', videoId : 'VY1eFxgRR-k'  },
        {  name: 'Mystery of love', videoId : '4WTt69YO2VI'  },
        {  name: 'Up', videoId : '29GWMT0GB6s'   },
        {  name: 'Unwritten', videoId : 'b7k0a5hYnSI'  },
        {  name: 'Lucky', videoId : 'acvIVA9-FMQ'  },
        {  name: 'I\'m yours', videoId : 'EkHTsc9PU2A'   },
        {  name: 'California', videoId : 'suYdhwmXASA'   },
        {  name: 'The way', videoId : '_sV0S8qWSy0'  },
        {  name: 'Lucky', videoId : 'acvIVA9-FMQ'  },
        {  name: 'I\'m yours', videoId : 'EkHTsc9PU2A'   },
        {  name: 'Sweet disposition', videoId : 'jxKjOOR9sPU'  },
      ],
      this.workout = [
        {  name: 'Overtime', videoId : '85ftfVUTzM4'  },
        {  name: 'Titanium', videoId : 'JRfuAukYTKg'  },
        {  name: 'I need your love', videoId : 'AtKZKl7Bgu0'  },
        {  name: 'Blood Sweat & Tears', videoId : 'hmE9f-TEutc'  },
        {  name: 'Dope', videoId : 'BVwAVbKYYeM'  },
        {  name: 'I don\'t like it, I love it', videoId : 'Tw8mpgccugc'  },
        {  name: 'Ain\'t got far to go', videoId : 'GxPcu7F7gWg'  },
        {  name: 'Rather be', videoId : 'm-M1AtrxztU'  },
        {  name: 'All I do is win', videoId : 'GGXzlRoNtHU'  },
        {  name: 'Can\'t hold us', videoId : 'VG3JsmOmDqw'  },
        {  name: 'Lonely together', videoId : 'vQ3XgMKAgxc'  },
        {  name: 'Stronger', videoId : 'Xn676-fLq7I'  },
        {  name: 'Run', videoId : '5Wn85Ge22FQ'  },
        {  name: 'Stronger faster better', videoId : 'PsO6ZnUZI0g'  },
        {  name: 'Bad blood', videoId : 'QcIy9NiNbmo'  },
        {  name: 'Stronger faster better', videoId : 'PsO6ZnUZI0g'  },
        {  name: 'Broken Arrows', videoId : 'V6iKSUoUN48'  },
      ],
      this.whatever = [
        {  name: 'Changing of the seasons', videoId : 'ovnCXhogusc'  },
        {  name: 'Next year', videoId : 'VTuJuok5QK4'  },
        {  name: 'Better by myself', videoId : 'aQgRkWG6q_g'  },
        {  name: 'Side Effects', videoId : 'nuckTcoZG4Q'  },
        {  name: 'Blame it on your love', videoId : 'y9Q4ttXokGs'  },
      ],
      this.chill = [
        {  name: 'What if I go?', videoId : 'pLuQ0MGLBXU'  },
        {  name: '1 Night', videoId : 'sjle_ZI4elo'  },
        
        {  name: 'Affection', videoId : 'uJoMqYumxmA'  },
        {  name: 'I wish I missed my ex', videoId : 'a7kT52xL-7g'  },
        {  name: 'Sober', videoId : 'jx96Twg-Aew'  },
        
        {  name: 'Better friends', videoId : 'j7vKsUYpvIQ'  },
        {  name: 'Cheapest flight', videoId : 'eCstDa1p_yE'  },
        {  name: 'Who\'s got you singing again', videoId : 'h-Yiku4Al48'  },
      ],
      this.upbeat = [
        {  name: 'Little talks', videoId : 'ghb6eDopW8I'  },
        {  name: 'Broke', videoId : 'fe0Enf31npc'  },
        {  name: 'Love me less', videoId : 'QO_Qz7ivhYQ'  },

      ],
      this.scared = [
        {  name: 'Doubt', videoId : 'RfgL_OaTomc'  },
        {  name: 'After the storm', videoId : '9f5zD7ZSNpQ'  },
        {  name: 'Houdini', videoId : '_GMQLjzVGfw'  },
      ],
      this.studying = [
        {  name: 'Han jan', videoId : 'A8S5Rd_02uA'  },
        {  name: 'Itgehane', videoId : 'SlbVgjFvE3I'  },
        {  name: 'Piano Concerto no.2 op.18', videoId : 'rEGOihjqO9w'  },
        {  name: 'Ce Bon Vieux Jean Lassalle', videoId : 'fSGtBqO1S0E'  },
        {  name: 'Do you want my love', videoId : 'J1SWn2IGOV4'  },
        {  name: 'Yamaha', videoId : 'OnW6rQ_z9Ug'  },
      ],
      this.powerwoman = [
        {  name: 'Oh No', videoId : 'Cr-SqRWImmI'  },
        {  name: 'Primadonna', videoId : 'Gj5L9SYhoSE'  },
        {  name: 'How to be a heartbreaker', videoId : 'vKNcuTWzTVw'  },
        {  name: 'Pop/Stars', videoId : 'UOxkGD8qRB4'  },
        {  name: 'Gonna get over you', videoId : 'OUe3oVlxLSA'  },
        {  name: 'Breakaway', videoId : 'c-3vPxKdj6o'  },
        {  name: 'Brave', videoId : 'QUQsqBqxoR4'  },
        {  name: 'King of anything', videoId : 'eR7-AUmiNcA'  },
      ],
      this.sad = [
        {  name: 'My Immortal', videoId : '5anLPw0Efmo'  },
        {  name: 'You found me', videoId : 'jFg_8u87zT0'  },
        {  name: 'Dream is destiny', videoId : 'o2zf28T0LFU'  },
        {  name: 'Nuclear mind', videoId : 'd7jiyAEb80M'  },
        {  name: 'Take me somewhere nice', videoId : 'luM6oeCM7Yw'  },
        {  name: 'Love for a child', videoId : 'X1gvLMz63Zc'  },
      ],
      this.french = [
        {  name: 'Tu Si Na Cosa Grande', videoId : '0cKCULV3WZ8'  },
        {  name: 'La Seine And I', videoId : 'S2V6jF79X7Q'  },
        {  name: 'Girl from Ipanema', videoId : 'sVdaFQhS86E'  },
        {  name: 'Amour T\'es Là ', videoId : 'JFkRtjrrM5k'   },
        {  name: 'Why try to change me now', videoId : '8uf1n1wUfxE'  },
        {  name: 'Fly me to the moon', videoId : 'qyqssZA9hww'  },
      ]

    },
    methods: {
      reset () {
        this.item = {}
      },
      selectFromParentComponent1 () {
        this.item = this.options[0]
      },
      pickMusic (mood) {
        var randomSongInd = Math.floor(Math.random() * this[mood].length);
        this.videoId = this[mood][randomSongInd].videoId;
        this.videoName = this[mood][randomSongInd].name;
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
.hello {
}
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
