<script lang="ts">
import { defineComponent } from 'vue';
import { parseToCurrentDay } from './Helpers/parseToCurrentDay';
import { parseDayToNewYear } from './Helpers/parseDayToNewYear';
import { parseTime } from './Helpers/parseTime';
import { TData } from './Interfaces/TData';
// import { Loader } from './UI/Loader/Loader.vue';

export default defineComponent({
  data(): TData {
    return {
      isShow: false,
      currentDay: '',
      daysToNewYear: '',
      time: '',
    };
  },
  mounted() {
    this.isShow = true;
    setInterval(() => {
      this.currentDay = parseToCurrentDay(new Date()),
      this.daysToNewYear = parseDayToNewYear(new Date()),
      this.time = parseTime(new Date())
      this.isShow = false;
    }, 1000);
  }
});
</script>

<template>
  <div class="app">
    <div v-if="isShow">
      <!-- <Loader></Loader> -->
      <div class="loader"></div>
    </div>
    <div v-else>
      <div class="title">
        <p class="subtitle">Новый год</p>
        <div class="subtitle">
          <p>{{ new Date().getFullYear() }}</p>
          <p>&#8594;</p>
          <p>{{ new Date().getFullYear() + 1 }}</p>
        </div>
        <div class="countdown">
          <p>{{ daysToNewYear }}</p>
          <p>{{ time }}</p>
        </div>
        <div>
          <p class="subtitle">{{ currentDay }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
@import url('https://db.onlinewebfonts.com/c/84cb021d5f9af287ffff84b61beef6dc?family=clockicons');

#root {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  text-align: center;
}

.loader {
    width: 60px;
    aspect-ratio: 1;
    color: #000;
    border: 10px solid;
    box-sizing: border-box;
    border-radius: 50%;
    animation: l6 2s infinite linear;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
.loader:before {
    content: "";
    position: absolute;
    height: 20px;
    inset: auto calc(50% - 10px) 100%;
    border-radius: 5px 5px 0 0;
    background: linear-gradient(currentColor 0 0) top/100% 30%, linear-gradient(currentColor 0 0) top/50% 100%;
    background-repeat: no-repeat;
}
.loader:after {
    content: "";
    position: absolute;
    inset: -8px -10px auto;
    height: 15px;
    background: radial-gradient(farthest-side,currentColor 94%,#0000) left, radial-gradient(farthest-side,currentColor 94%,#0000) right;
    background-size: 15px 15px;
    background-repeat: no-repeat;
}
@keyframes l6 {
    0%   {background: conic-gradient(#77a4bd 0     ,#0000 0)}
    12.5%{background: conic-gradient(#77a4bd 45deg ,#0000 46deg)}
    25%  {background: conic-gradient(#77a4bd 90deg ,#0000 91deg)}
    37.5%{background: conic-gradient(#77a4bd 135deg,#0000 136deg)}
    50%  {background: conic-gradient(#77a4bd 180deg,#0000 181deg)}
    62.5%{background: conic-gradient(#77a4bd 225deg,#0000 226deg)}
    75%  {background: conic-gradient(#77a4bd 270deg,#0000 271deg)}
    87.5%{background: conic-gradient(#77a4bd 315deg,#0000 316deg)}
    100% {background: conic-gradient(#77a4bd 360deg,#0000 360deg)}
}

.app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.title {
  margin: 100px 0 50px 0;
  text-align: center;
}

.subtitle {
  font-size: 25px;
  display: flex;
  justify-content: center;
  gap: 20px;
}

.countdown {
  display: flex;
  justify-content: center;
  gap: 10px;
}

.countdown > p {
  font-family: "clockicons", sans-serif;
  margin: 20px 0;
  font-size: 50px;
}

.countdown span {
  font-size: 25px;
}
</style>