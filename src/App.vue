<script setup>
import UAParser from "ua-parser-js";
import { computed, ref } from "vue";

const searchParams = new URLSearchParams(window.location.search);
const ua = searchParams.get("ua") ?? "";
console.log(ua);

const input = ref(ua);
const output = computed(() => JSON.stringify(new UAParser(input.value).getResult(), null, 2));

const onChange = () => {
  const url = new URL(window.location);
  if (input.value) {
    url.searchParams.set("ua", input.value);
  } else {
    url.searchParams.delete("ua");
  }
  console.log(url);
  window.history.replaceState(null, "", url);
};
</script>

<template>
  <main>
    <input type="text" v-model="input" @change="onChange" autofocus />
    <textarea :value="output" readonly></textarea>
  </main>
</template>

<style scoped>
</style>
