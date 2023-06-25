<template>
  <q-page class="flex column items-center">
    <section class="flex q-mt-xl">
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

const socket = io("http://localhost:3001");

const message = ref();

const send = async () => {
  socket.emit("message", message.value);
  message.value = null;
};
</script>
