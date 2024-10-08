<template>
  <div class="chat-window">
    <h2>{{ user }}</h2>
    <div class="message-list">
      <div v-for="(msg, index) in messages" :key="index" class="message">
        <strong>{{ msg.user }}:</strong> {{ msg.message }}
        <small>{{ msg.timestamp }}</small>
      </div>
    </div>
    <input
      v-model="newMessage"
      placeholder="Напишите сообщение"
      @keyup.enter="sendMessage"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";

// Пропсы
const props = defineProps({
  user: String,
  messages: Array,
});

// Локальное состояние для ввода нового сообщения
const newMessage = ref("");

// Отправка сообщения
const emit = defineEmits(["sendMessage"]);
const sendMessage = () => {
  if (newMessage.value.trim() !== "") {
    emit("sendMessage", props.user, newMessage.value);
    newMessage.value = ""; // Очистка поля ввода
  }
};
</script>

<style scoped>
.chat-window {
  width: 300px;
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 5px;
}

.message-list {
  height: 200px;
  overflow-y: auto;
  margin-bottom: 10px;
  border: 1px solid #eee;
  padding: 10px;
  border-radius: 5px;
}

.message {
  margin-bottom: 10px;
}

input {
  width: 100%;
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
}
</style>
