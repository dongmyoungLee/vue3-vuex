<template>
  <div class="search-bar">
    <form @submit.prevent>
      <div class="form-group">
        <input @input="inputText = $event.target.value" type="search" placeholder="지역을 입력해 주세요">
        <button @click="
        store.onSearchCity(inputText);
        store.getWeather();
        // $store.commit('onSearchCity', inputText);
        // $store.dispatch('getWeather');
        ">
          <font-awesome-icon class="icon" :icon="['fas', 'magnifying-glass']" />
        </button>
      </div>
    </form>
  </div>
</template>

<script setup>

  import {ref} from "vue";
  import useStore from "@/store/piniaStore.js";
  import {storeToRefs} from "pinia";

  const inputText = ref('');
  const emits = defineEmits(['onSearchCity'])

  const store = useStore();
  const { weatherData, toggle } = storeToRefs(store);

</script>

<style lang="scss" scoped>
.search-bar {
  padding: 8px 20px;
  border-radius: 40px;
  background: #fff;
  border: 1px solid #ccc;
  padding: 0 20px;

  form {
    .form-group {
      display: flex;
      input {
        width: 100%;
        border: none;
        padding: 1em 0;
        font-size: 18px;
        outline: none;
        font-size: 14px;
      }
      button {
        background: transparent;
        border: none;
        &:hover { cursor: pointer; }
        .icon { font-size: 24px; }
      }
    }
  }
}
</style>
