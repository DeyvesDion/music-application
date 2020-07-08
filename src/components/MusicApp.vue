<template>
 <div class="container">
  <div class="card mt-5 mb-5">
   <div class="card-header">
    <div class="custom-control custom-switch">
     <input
      v-model="turnOn"
      type="checkbox"
      class="custom-control-input"
      id="customSwitch"
     />
     <label class="custom-control-label" for="customSwitch">Power</label>
    </div>
    <div class="form-group rangeGroup">
     <label for="volume">Volume</label>
     <input
      v-model="volume"
      type="range"
      min="0"
      max="5"
      class="f ml-5"
      id="volume"
     />
    </div>
    <div class="currentMusicTitle border px-4 my-2">
     <h5>{{ currentMusicTitre }}</h5>
    </div>
   </div>
   <div class="card-body">
    <h5 class="card-title text-center">Playlist</h5>
    <hr />
    <div class="row musicCardGroup">
     <div v-for="music in Musics" :key="music.Titre" class="musicCard">
      {{ music.Titre }}
      <div class="playStop mt-3">
       <!-- play btn -->
       <svg
        :class="[{ turnOFF: !turnOn }]"
        @click="playMusic(music)"
        width="1.5em"
        height="1.5em"
        viewBox="0 0 16 16"
        class="bi bi-play mr-3"
        fill="currentColor"
        xmlns="http://www.w3.org/2000/svg"
       >
        <path
         fill-rule="evenodd"
         d="M10.804 8L5 4.633v6.734L10.804 8zm.792-.696a.802.802 0 0 1 0 1.392l-6.363 3.692C4.713 12.69 4 12.345 4 11.692V4.308c0-.653.713-.998 1.233-.696l6.363 3.692z"
        />
       </svg>

       <!-- stop btn -->
       <svg
        :class="[{ turnOFF: !turnOn }]"
        @click="stopMusic(music)"
        width="1.5em"
        height="1.5em"
        viewBox="0 0 16 16"
        class="bi bi-stop"
        fill="currentColor"
        xmlns="http://www.w3.org/2000/svg"
       >
        <path
         fill-rule="evenodd"
         d="M3.5 5A1.5 1.5 0 0 1 5 3.5h6A1.5 1.5 0 0 1 12.5 5v6a1.5 1.5 0 0 1-1.5 1.5H5A1.5 1.5 0 0 1 3.5 11V5zM5 4.5a.5.5 0 0 0-.5.5v6a.5.5 0 0 0 .5.5h6a.5.5 0 0 0 .5-.5V5a.5.5 0 0 0-.5-.5H5z"
        />
       </svg>
      </div>
     </div>
    </div>
   </div>
  </div>
 </div>
</template>

<script>
import Musics from "./Musics";
export default {
 name: "MusicApp",
 data() {
  return {
   Musics,
   volume: 2,

   turnOn: true,
   currentMusicTitre: "Pas de music",
  };
 },
 methods: {
  playMusic(music) {
   if (this.turnOn) {
    let m = new Audio(music.Url);
    m.play();
    m.volume = this.volume / 5;
    this.currentMusicTitre = music.Titre;
    this.currentMusic = m;
   }
  },
  stopMusic(music) {
   this.currentMusic.pause(music);
  },
 },
};
</script>

<style src="./MusicApp.css" scoped></style>
