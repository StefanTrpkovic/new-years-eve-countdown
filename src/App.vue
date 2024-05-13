<script setup>
import { reactive } from "vue";
import CountdownHeader from "@/components/CountdownHeader.vue";
import CountdownSegment from "@/components/CountdownSegment.vue";

// Set the date we're counting down to
const countDownDate = new Date("Jan 1, 2025 00:00:00").getTime();

const time = reactive({
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0,
});

// Update the count down every 1 second
const x = setInterval(function () {
  // Get today's date and time
  var now = new Date().getTime();

  // Find the distance between now and the count down date
  var distance = countDownDate - now;

  // Calculate days, hours, minutes, and seconds
  time.days = Math.floor(distance / (1000 * 60 * 60 * 24));
  time.hours = Math.floor(
    (distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
  );
  time.minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
  time.seconds = Math.floor((distance % (1000 * 60)) / 1000);

  // Display the result
  console.log(time.days + "d " + time.hours + "h " + time.minutes + "m " + time.seconds + "s");

  // If the countdown is over, display a message
  if (distance < 0) {
    clearInterval(x);
    console.log("Happy New Year!");
  }
}, 1000);
</script>
<template>
  <div class="app-wrapper">
    <div class="countdown-box">
      <CountdownHeader />
      <main class="flex justify-center">
        <CountdownSegment data-test="days" label="days" :number="time.days" />
        <CountdownSegment
          data-test="hours"
          label="hours"
          :number="time.hours"
        />
        <CountdownSegment
          data-test="minutes"
          label="minutes"
          :number="time.minutes"
        />
        <CountdownSegment
          data-test="seconds"
          label="seconds"
          :number="time.seconds"
        />
      </main>
    </div>
  </div>
</template>

<style scoped>
.app-wrapper {
  @apply flex items-center justify-center w-full h-full p-10;
}
.countdown-box {
  @apply shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px];
}
body {
  @apply bg-gray-100;
}
</style>
