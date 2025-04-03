<script setup>
import Navbar from './components/Navbar.vue';
import MainComp from './components/MainComp.vue';
import About from './components/About.vue';
import {onMounted, ref, computed} from 'vue';
import useStore from './store/piniaStore.js';
import {storeToRefs} from "pinia";

// vuex
// const store = useStore();

// pinia
const store = useStore();
const { weatherData, toggle } = storeToRefs(store);

// 앱이 실행되면 날씨 데이터 가져오기
onMounted(() => {
  // store.dispatch('getWeather');
  store.getWeather();
  console.log("asdasdasd")
})

const onSearchCity = (city) => {
  weatherData.value.city = city;
  getWeather();
}

const count = ref(0);
const title = ref('title');
const number= ref(0);

// number 가 변경될때 자동계산
const result = computed(() => {
  return number.value * 2;
})

const pay = ref(null);
const tax = 3.3;

const myPay = computed(() => {
  return pay.value - (tax / 100) * pay.value;
})

</script>

<template>
  <!-- <button @click="$store.dispatch('getWeather')">getWeather</button> -->
  <p>{{count}}</p>
  <p>{{title}}</p>
  <p>{{number}}</p>
  <p>{{result}}</p>
  <button @click="count++">증가</button>
  <input v-model="pay" placeholder="수입" />
  <p>실수령액 : {{myPay}}</p>
  <Navbar v-model="title" />
  <div v-if="!toggle">
    <MainComp/>
  </div>
  <div v-else>
    <About />
  </div>
</template>

<style scoped lang="scss">

</style>