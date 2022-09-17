<template>
  <v-app>
    <v-main>
      <v-container-fluid>
        <v-row class="justify-center py-3">
          <v-col cols="12" class="black white--text">
            <h1 class="text-center">My Music</h1>
          </v-col>

          <v-col class="col-12 mt-3">
            <h1 class="text-center font-weight-bold">
              {{ this.current.title }} - <span>{{ this.current.artist }}</span>
            </h1>
          </v-col>

          <v-col cols="12" class="mx-auto text-center mt-3">
            <v-btn fab class="mx-10 primary" @click="prev">
              <v-icon>mdi-skip-previous</v-icon>
            </v-btn>
            <v-btn
              class="mx-10 primary"
              fab
              large
              @click="play"
              v-if="!isPlaying"
            >
              <v-icon dark>mdi-play</v-icon>
            </v-btn>
            <v-btn class="mx-10 primary" fab large @click="pause" v-else>
              <v-icon>mdi-pause</v-icon>
            </v-btn>
            <v-btn class="mx-10 primary" fab @click="next">
              <v-icon>mdi-skip-next</v-icon>
            </v-btn>
          </v-col>

          <v-col cols="12" class="text-center">
            <h1 class="my-5">The Playlist</h1>
            <v-btn
              v-for="song in songs"
              :key="song"
              x-large
              class="pink darken-1 white--text songlists my-1"
              @click="play(song)"
            >
              {{ song.title }} - {{ song.artist }}
            </v-btn>
          </v-col>
        </v-row>
      </v-container-fluid>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    current: {},
    isPlaying: false,
    index: 0,
    songs: [
      {
        title: "အဓိပ္ပာယ်",
        artist: "Idiots",
        src: require("./assets/idiots (1).mp3"),
      },
      {
        title: "အသက်ငွေ့ငွေ့",
        artist: "Idiots",
        src: require("./assets/idiots (2).mp3"),
      },
      {
        title: "မင်းနဲ့နီးဖို့",
        artist: "Idiots",
        src: require("./assets/idiots (3).mp3"),
      },
      {
        title: "ငါ့အပြစ်နဲ့ငါ",
        artist: "Idiots",
        src: require("./assets/idiots (4).mp3"),
      },
      {
        title: "နောက်ကျော",
        artist: "Idiots",
        src: require("./assets/idiots (5).mp3"),
      },
      {
        title: "ဆုလာဒ်",
        artist: "Idiots",
        src: require("./assets/idiots (6).mp3"),
      },
      {
        title: "တစ်စုံတစ်ရာ",
        artist: "Idiots",
        src: require("./assets/idiots (7).mp3"),
      },
      {
        title: "တွေ့ရတာဝမ်းသာတယ်",
        artist: "Idiots",
        src: require("./assets/idiots (8).mp3"),
      },
      {
        title: "ဝမ်းနည်းတက်တဲ့ချစ်သူ",
        artist: "Idiots",
        src: require("./assets/idiots (9).mp3"),
      },
      {
        title: "ချန်ခဲ့",
        artist: "Idiots",
        src: require("./assets/Idiots-Collection-2.mp3"),
      },
      {
        title: "အချိန်တန်တော့",
        artist: "Idiots",
        src: require("./assets/Idiots-Collection-4.mp3"),
      },
      {
        title: "အတု",
        artist: "Idiots",
        src: require("./assets/Idiots-Collection-15.mp3"),
      },
      {
        title: "မင်းအတွက်မင်း",
        artist: "Idiots",
        src: require("./assets/Idiots-Collection-17.mp3"),
      },
      {
        title: "သိပ်ကြောက်လို့",
        artist: "Idiots",
        src: require("./assets/Idiots-Collection-18.mp3"),
      },
      {
        title: "ထပ်မမေးနဲ့တော့",
        artist: "Idiots",
        src: require("./assets/Idiots-Collection-19.mp3"),
      },
    ],
    player: new Audio(),
  }),
  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener(
        "ended",
        function () {
          this.index++;
          if (this.index > this.songs.length - 1) {
            this.index = 0;
          }
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
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  },
};
</script>

<style>
.songlists {
  width: 80%;
}
</style>
