<template>
  <div id="app">
    <div class="desktop-icons">
      <win311-icon class="desktopicon" name="msdos"></win311-icon>
    </div>
    <win311-window class="first" type="apps"></win311-window>
    <win311-window class="second" type="cpanel"></win311-window>
  </div>
</template>

<script>
import Vue from "vue";
import Win311Icon from "@/components/Win311Icon.vue";
import Win311Window from "@/components/Win311Window.vue";
import Win311Error from "@/components/Win311Error.vue";
import audio from "@/assets/mp3/w31-error.mp3";
import titanic from "@/assets/mp3/titanic-flauta.mp3";
import bsodImg from "@/assets/bsod.png";
import { Howl } from "howler";

var count = 0;
var sound = new Howl({
  src: [audio],
});

var bsodSound = new Howl({
  src: [titanic],
});

export default {
  name: "App",
  components: {
    "win311-window": Win311Window,
    "win311-icon": Win311Icon,
  },
  methods: {
    displayErrors(time) {
      if (time > 0) {
        setTimeout(() => {
          this.mountError(time);
        }, time);
      } else {
        setTimeout(() => {
          bsodSound.play();
          let bsod = document.createElement("img");
          bsod.setAttribute("src", bsodImg);
          bsod.style.width = "100%";
          bsod.style.height = "100%";
          bsod.style.position = "absolute";
          // z-index cuanto más alto mejor, por si acaso
          bsod.style.zIndex = "99999999";
          this.$el.appendChild(bsod);
        }, 1250);
      }
    },
    mountError(time) {
      sound.play();
      let ComponentClass = Vue.extend(Win311Error);
      let instance = new ComponentClass();
      instance.$mount();
      let top = Math.floor(Math.random() * 524);
      let left = Math.floor(Math.random() * 1248);

      instance.$el.style.top = `${top}px`;
      instance.$el.style.left = `${left}px`;
      this.$el.appendChild(instance.$el);

      if (time > 1000) {
        time -= 150;
      } else if (time > 500) {
        time -= 75;
      } else if (time > 100) {
        time -= 15;
      } else {
        time -= 5;
      }

      this.displayErrors(time);
    },
    count() {
      count++;
      if (count === 3) {
        this.displayErrors(1500, 20);
      }
    },
  },
  mounted() {
    this.evlistener = this.$el.addEventListener("dblclick", this.count);
  },
};
</script>

<style lang="postcss">
#app {
  background-color: #0fa8db;
  height: 100vh;
}

body {
  margin: 0;
  overflow-x: hidden;
}

.desktop-icons {
  width: 100%;
  height: 96%;
  position: absolute;
}

.first {
  left: 200px;
  top: 50px;
}
.second {
  top: 300px;
  left: 650px;
}
</style>
