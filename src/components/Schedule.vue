<script setup>
import { onMounted } from "@vue/runtime-core";
import app from "../App.vue";
setTimeout(() => {
  app.load(1);
}, 2000);
</script>

<template>
  <div
    class="wrapper p-4 lg:p-[4_8_10_8] pb-6 max-w-2xl lg:max-w-full grid gap-x-4 grid-cols-[1fr_3fr] lg:grid-cols-[1fr_5fr] overflow-x-auto"
  ></div>
</template>

<style>
.wrapper::-webkit-scrollbar {
  display: none;
}
.lecture {
  box-shadow: 0px 4px 24px rgba(0, 0, 0, 0.08);
  width: 12rem;
  border-radius: 12px;
  padding: 12px;
  padding-bottom: 3rem;
  margin-top: 1.5rem;
  position: relative;
}
.lectures {
  display: flex;
}
.lectures div {
  margin-right: 1rem;
}
.room {
  background-color: #ff7518;
  width: fit-content;
  padding: 2px 8px;
  border-radius: 6px;
  font-weight: 700;
  font-size: 0.8rem;
  position: absolute;
  right: 12px;
  bottom: 12px;
}
.timing {
  background-color: inherit;
  font-family: "DM Sans", sans-serif;
  font-weight: 500;
  padding-top: 2rem;
  min-width: 6rem;
}
</style>
