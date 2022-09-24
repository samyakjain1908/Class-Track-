<script setup>
import app from "../App.vue";

const week = [
  "monday",
  "tuesday",
  "wednesday",
  "thursday",
  "friday",
  "saturday",
];
const changeDay = function (element) {
  if (!element.classList.contains("active")) {
    document.querySelector(".wrapper").innerHTML = "";
    document.querySelectorAll(".day").forEach((day) => {
      day.classList.remove("active");
    });
    element.classList.toggle("active");

    week.forEach((day, i) => {
      if (element.id == day) app.load(i + 1);
    });
  }
};
</script>

<template>
  <nav class="px-2 pb-4 max-w-2xl flex justify-between overflow-x-auto sticky">
    <div
      id="monday"
      @click="changeDay($event.target)"
      class="day dark:text-white active rounded-full"
    >
      Monday
    </div>
    <div
      id="tuesday"
      @click="changeDay($event.target)"
      class="day dark:text-white rounded-full"
    >
      Tuesday
    </div>
    <div
      id="wednesday"
      @click="changeDay($event.target)"
      class="day dark:text-white rounded-full"
    >
      Wednesday
    </div>
    <div
      id="thursday"
      @click="changeDay($event.target)"
      class="day dark:text-white rounded-full"
    >
      Thursday
    </div>
    <div
      id="friday"
      @click="changeDay($event.target)"
      class="day dark:text-white rounded-full"
    >
      Friday
    </div>
    <div
      id="saturday"
      @click="changeDay($event.target)"
      class="day dark:text-white rounded-full"
    >
      Saturday
    </div>
  </nav>
</template>
<style scoped>
nav::-webkit-scrollbar {
  display: none;
}
.day {
  scroll-behavior: smooth;
  display: inline;
  font-weight: 600;
  border: 2px solid #ff7518;
  padding: 0.25rem 0.75rem;
  margin: 0 0.3rem;
  cursor: pointer;
}

.active {
  background: #ff7518;
  color: white;
}
</style>
