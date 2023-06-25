<template>
  <q-page class="flex column items-center">
    <section class="flex q-mt-xl">
      <q-input v-model="room" type="number" />
      <q-input
        v-model="message"
        type="text"
        class="q-mr-md"
        @keyup.enter="send()"
      />
      <q-btn dense flat @click="send()">Отправить</q-btn>
    </section>
  </q-page>
</template>

<script setup>
import { ref } from "vue";
import { io } from "socket.io-client";

const socket = io("http://localhost:3001", {
  auth: {
    token: "secret1",
  },
});

const message = ref();
const room = ref(1);

socket.on("message", (data) => {
  console.log(data);
});

socket.on("connect_error", (data) => {
  console.error(data);
});

const send = async () => {
  socket.emit("message", {
    message: message.value,
    room: room.value,
  });
  message.value = null;
};
</script>
