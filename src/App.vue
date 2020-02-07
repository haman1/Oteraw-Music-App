<template>
  <div id="app">
    <header>
      <h1>Mziki yangu</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span></h2>
        <div class="controls">
          <button class="Prev" @click="previous">previous</button>
          <button class="play" v-if="!isPlaying" @click="play">play</button>
          <button class="pause" v-else @click="pause">pause</button>
          <button class="Next" @click="Next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>Playlist ya Oteraw(Herman)</h3>
        <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src== current.src) ? 'song playing' : 'song'">
          {{ song.title }} - {{ song.artist }}
        </button>
       
      </section>
    </main>
  </div>
</template>

<script>


export default {
  name: 'App',
  data () {
    return {
      current:{},
      index: 0,
      isPlaying: false,
      songs: [
        {
        title: "saa zingine",
        artist: "Didge",
        src: require('./assets/03 saa zingine.mp3')
      },
       
    {
    title: "Someday",
    artist: "Atemi Oyungu Ft Chris Adwar",
     src: require('./assets/Artist - Track 03.mp3')
      },
       {
        title: "Usinibore",
        artist: "Just_a_band",
        src: require('./assets/Just_A_Band-Usinibore.mp3')
      },
       {
        title: "Hahe",
        artist: "Just_a_band",
        src: require('./assets/just_a_band-hahe.mp3')
      },
      {
        title: "Haiya",
        artist: "Harry Kimani",
        src: require('./assets/11 Haiya.mp3')
      },
      {
        title: "True story",
        artist: "kitu sewer",
        src: require('./assets/frank-mteule_true-story-feat-kitu-sewer.mp3')
      },
      {
        title: "Uongo",
        artist: "kitu sewer",
        src: require('./assets/sniper-g-ganji_uongo-kitu-sewer-ft-kevmamba-washamba-wenza.mp3')

      },
      {
        title: "Feel Free",
        artist: "kitu sewer",
        src: require('./assets/Ukoo FLani Mau Mau-Feel free.mp4')

      },
      ],
      player: new Audio()

    }
  },
  methods:{
    play (song) {
      if (typeof song.src != "undefined") {
        this.current =song;

        this.player.src = this.current.src;
      }
       this.player.play();
       this.player.addEventListener('ended', function () {
         this.index++;
         if (this.index > this.songs.length -1) {
        this.index =0;
      }
       this.current = this.songs[this.index];
      this.play(this.current);
    
    
       }.bind(this));
       this.isPlaying = true;
    },
    pause (){
      this.player.pause();
    this.isPlaying = false;

    },
     Prev (){
     this.index--;
      if (this.index < 0)  {
        this.index = this.songs[this.songs.length -1];
      }
      this.current = this.songs[this.index];
      this.play(this.current);

    },
     Next (){
      this.index++;
      if (this.index > this.songs.length -1) {
        this.index =0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    }
    
    
    
  },
  created () {
  this.current = this.songs[this.index];
  this.player.src = this.current.src;
  //this.player.play();
}
}
  

</script>

<style>
*{
  margin:0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
}
header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: #212121;
  color: #FFF;

}
main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding:  25px;

}
.song-title{
  color: #212121;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}
.song-title span{
  font-weight: 400;
  font-style: italic;

}
.controls{
  display: flex;
justify-content: center;
align-items: center;
padding: 30px 15px;

}

button {
  appearance: none;
  background: none;
  border:none;
  outline: none;
  cursor: pointer;
}
button:hover{
  opacity: 0.8;
}

.play{
  font-size: 20px;
  font-weight: 700px;
  padding: 15px 25px;
  margin : 0px 15px;
  border-radius: 8px;
  color : #FFF;
  background-color: #CC2E50;

}
.next, .prev {
  font-size: 16px;
  font-weight: 700px;
  padding: 10px 20px;
  margin : 0px 15px;
  border-radius: 6px;
  color : #FFF;
  background-color:#FF5733;

}
.playlist {
  padding: 0px 30px;

}
.playlist h3{
  color:#212121;
  font-size: 18px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}
.playlist .song {
  display: black;
  width: 100;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;

}
.playlist .song.playing {
  color: white;
  background-image: 
}


</style>
