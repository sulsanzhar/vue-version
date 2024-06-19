<script lang="ts">
import { parseToCurrentDay } from './Helpers/parseToCurrentDay';
import { parseDayToNewYear } from './Helpers/parseDayToNewYear';
import { parseTime } from './Helpers/parseTime';
import { TData } from './Interfaces/TData';
import Loader from './UI/Loader/Loader.vue';

export default {
  components: {
    Loader
  },
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
};
</script>

<template>
  <div class="app">
    <div v-if="isShow">
      <Loader/>
      <!-- <div class="loader"></div> -->
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