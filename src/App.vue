<template>
  <div id="app">
    <header>
      <h1>Surah</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="surah-title">{{ current.title }} - <span> {{ current.artist }}</span></h2>
        <div class="control">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
        <button v-for="surah in surahs" :key="surah.src" @click="play(surah)" :class="(surah.src == current.src) ? 'Surah Playing' : 'Surah'">
          {{ surah.title }} - {{ surah.artist }}
        </button>
      </section>
    </main>
  </div>
</template>

<script>

export default {
  
  data () {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      surahs:[
        {
          title: 'Surah Fatiha',
          artist: 'Nasser Al Qatami',
          src: require('./assets/001-Surah-Fatihah.mp3'),
        },
        {
          title: 'Surah Al-Falaq',
          artist: 'Nasser Al Qatami',
          src: require('./assets/113-Surah-Al-Falaq.mp3'),
        },
        {
          title: 'Surah An-Nas',
          artist: 'Nasser Al Qatami',
          src: require('./assets/114-Surah-An-Nas.mp3'),
        },
      ],
      player: new Audio(),
    }
  },
  created() {
    this.current = this.surahs[this.index];
    this.player.src = this.current.src;
    // this.player.play();
  },
  methods: {
    play(surah) {
      if (typeof surah.src != 'undefined') {
        this.current = surah;

        this.player.src = this.current.src;
      }

      this.player.play();
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next () {
      this.index++;
      if (this.index > this.surahs.length - 1 ) {
        this.index = 0;
      }

      this.current = this.surahs[this.index];

      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0 ) {
        this.index = this.songs.length - 1;
      }

      this.current = this.surahs[this.index];

      this.play(this.current);
    }
  },
}
</script>

<style>

  /*  */
  * {
    margin: 0;
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


</style>
