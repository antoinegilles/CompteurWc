<template>
  <v-app>
    <v-app-bar app color="brown" dark>
      <div class="d-flex align-center">
        <h2>Poop</h2>
      </div>
    </v-app-bar>

    <v-main>
      <transition name="fade">
        <div @click="run" v-if="validate == false">
          <div class="mouches">
            <img class="mouche" src="./assets/mouche.png" alt="" />
            <img class="mouche2" src="./assets/mouche.png" alt="" />
          </div>
          <p class="poop">
            <img class="crotte" src="./assets/crotte.png" />
          </p>
        </div>
      </transition>
      <div v-if="validate">
        <Poop />
      </div>
      <div v-else></div>
    </v-main>
  </v-app>
</template>

<script>
import Poop from "./components/Poop";

export default {
  name: "App",

  components: {
    Poop,
  },

  data: () => ({
    validate: false,
  }),
  methods:{
    run(){
      this.validate = true
      const audio = new Audio(require('./assets/pet.mp3'))
      audio.play()
    }
  }
};
</script>
<style scoped>
@keyframes voler {
  0% {
    top: 6em;
  }
  50% {
    top: 8em;
  }
  100% {
    top: 6em;
  }
}
@keyframes voler2 {
  0% {
    top: 15em;
  }
  50% {
    top: 13em;
  }
  100% {
    top: 15em;
  }
}

.mouche {
  position: relative;
  transform: scaleX(-1);
  animation-name: voler;
  animation-duration: 4s;
  animation-iteration-count: infinite;
  width: 5em;
  margin-left: 40%;
}
.mouche2 {
  position: relative;
  animation-name: voler2;
  animation-duration: 7s;
  animation-iteration-count: infinite;
  width: 5em;
}
.poop {
  text-align: center;
}
.crotte {
  width: 25em;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.4s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
