<template>
  <div id="app">
    <header>
      <h1>Surah</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="surah-title">
          {{ current.title }} - <span> {{ current.artist }}</span>
        </h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
        <button
          v-for="surah in surahs"
          :key="surah.src"
          @click="play(surah)"
          :class="surah.src == current.src ? 'Surah Playing' : 'surah'"
        >
          {{ surah.title }} - {{ surah.artist }}
        </button>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      surahs: [
        {
          title: "Surah Fatiha",
          artist: "Nasser Al Qatami",
          src: require("./assets/001-Surah-Fatihah.mp3"),
        },
        {
          title: "Surah Al-Falaq",
          artist: "Nasser Al Qatami",
          src: require("./assets/113-Surah-Al-Falaq.mp3"),
        },
        {
          title: "Surah An-Nas",
          artist: "Nasser Al Qatami",
          src: require("./assets/114-Surah-An-Nas.mp3"),
        },
      ],
      player: new Audio(),
    };
  },
  created() {
    this.current = this.surahs[this.index];
    this.player.src = this.current.src;
    // this.player.play();
  },
  methods: {
    play(surah) {
      if (typeof surah.src != "undefined") {
        this.current = surah;

        this.player.src = this.current.src;
      }

      this.player.play();
      this.player.addEventListener(
        "ended",
        function () {
          this.index++;
          if (this.index > this.surahs.length - 1) {
            this.index = 0;
          }

          this.current = this.surahs[this.index];
          this.play(this.current);
        }.bind(this)
      );
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++;
      if (this.index > this.surahs.length - 1) {
        this.index = 0;
      }

      this.current = this.surahs[this.index];

      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }

      this.current = this.surahs[this.index];

      this.play(this.current);
    },
  },
};
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
  color: #fff;
}

main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}

.surah-title {
  color: #212121;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.surah-title span {
  font-weight: 400;
  font-style: italic;
}

.controls {
  display: flex;
  justify-content: center;
  padding: 30px 15px;
}

button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}

button.hover {
  opacity: 0.8;
}

.play,
.pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
  background-color: #cc2e5d;
}

.next,
.prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #fff;
  background-color: #ff5858;
}

.playlist {
  padding: 0px 30px;
}

.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}

.playlist .surah {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}

.playlist .surah:hover {
  color: #ff5858;
}

.playlist .surah.playing {
  color: #fff;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
}
</style>
