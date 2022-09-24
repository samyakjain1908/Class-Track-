<script setup>
import Header from "./components/Header.vue";
import weekSlider from "./components/weekSlider.vue";
import Schedule from "./components/Schedule.vue";
import Footer from "./components/Footer.vue";
</script>

<template>
  <div class="max-w-6xl mx-auto">
    <Header page="Timetable" />
    <Schedule />
    <Footer />
  </div>
</template>

<style scoped></style>

<script>
import $ from "jquery";
var dataset;

$.get(
  "https://script.google.com/macros/s/AKfycbzyGRrtgNJT69sl-RIigZwqDKWaiH1mGnG04oafvBO9MUpbH3cAwv0ywiRVM5pGx1h3/exec",
  function (data) {
    localStorage.data = JSON.stringify(data.data.slice(1));
  }
);
setInterval(() => {
  $.get(
    "https://script.google.com/macros/s/AKfycbzyGRrtgNJT69sl-RIigZwqDKWaiH1mGnG04oafvBO9MUpbH3cAwv0ywiRVM5pGx1h3/exec",
    function (data) {
      localStorage.data = JSON.stringify(data.data.slice(1));
    }
  );
}, 15000);

const loadSchedule = function (day) {
  const timings = [
    "8:00 am",
    "9:00 am",
    "10:30 am",
    "11:30 am",
    "1:30 pm",
    "2:30 pm",
    "4:00 pm",
    "5:00 pm",
    "5:00 pm to 7:00 pm",
  ];

  dataset = JSON.parse(localStorage.data);

  dataset.forEach((slot, j) => {
    var period = slot[day];
    if (period !== "") {
      let timeSlot = document.createElement("section");
      let lectures = document.createElement("section");

      timeSlot.innerText = timings[j];
      timeSlot.classList.add("timing");
      timeSlot.classList.add("text-[#555]");
      timeSlot.classList.add("dark:text-[#f9f9f9]");
      lectures.classList.add("lecture");

      let i = 0,
        flag = true;
      while (i <= period.length) {
        if (period[i] == "+") {
          lectures.classList.replace("lecture", "lectures");
          let lecture = document.createElement("div");
          let lecRoom = document.createElement("section");
          lecRoom.classList.add("room");
          lecRoom.classList.add("text-white");
          lecRoom.classList.add("dark:text-[#282828]");
          lecture.classList.add("lecture");
          lecture.classList.add("bg-white");
          lecture.classList.add("dark:bg-[#282828]");
          lecture.classList.add("dark:text-white");
          lecRoom.innerText = period.slice(i - 4, i);
          lecture.innerHTML = period.slice(0, i - 4);
          lecture.appendChild(lecRoom);
          lectures.appendChild(lecture);
          period = period.slice(i + 2);
          i = 0;
          flag = false;
        }
        i++;
      }
      if (flag) {
        let lecture = document.createElement("div");
        let lecRoom = document.createElement("section");
        lecRoom.classList.add("room");
        lecRoom.classList.add("text-white");
        lecRoom.classList.add("dark:text-[#282828]");
        lectures.classList.add("bg-white");
        lectures.classList.add("dark:bg-[#282828]");
        lectures.classList.add("dark:text-white");
        lecture.innerHTML = period.slice(0, -4);
        lecRoom.innerText = period.slice(-3);
        lecture.appendChild(lecRoom);
        lectures.innerHTML = lecture.innerHTML;
      }

      document.querySelector(".wrapper").appendChild(timeSlot);
      document.querySelector(".wrapper").appendChild(lectures);
    }
  });
};

export default {
  dataset: dataset,
  load: loadSchedule,
};
</script>
