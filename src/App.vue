<template>
  <router-view />
</template>

<script setup>
import { defineComponent } from "vue";
import { io } from "socket.io-client";

const socket = io("http://localhost:3001");
</script>
