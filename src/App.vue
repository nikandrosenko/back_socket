<template>
  <router-view :socket="socket" />
</template>

<script setup>
import { defineComponent } from "vue";
import { io } from "socket.io-client";

const socket = io("http://localhost:3001");

socket.on("connected", (arg) => {
  console.log(arg);
});

socket.on("disconnect", (reason) => {
  console.log("Соединение разорвано... ", reason);
});
</script>
