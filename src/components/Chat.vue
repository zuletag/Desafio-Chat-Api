<template>
    <div class="chat-box p-3 border rounded mb-3">
      <div v-for="(message, index) in messages" :key="index" :class="message.sender === 'Person A' ? 'text-left' : 'text-right'">
        <div>
            <span>{{ message.sender === 'Person A' ? userA?.name.first : userB?.name.first }}:</span>
        </div>
        <div :style="{ backgroundColor: message.color }" class="message-bubble d-inline-block p-2 mb-2 rounded text-white">
            {{ message.text }}
        </div>
        <div style="clear: both;"></div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['messages', 'userA', 'userB'], // Recibe mensajes, usuario A y usuario B del componente padre
  };
  </script>
  
  <style scoped>
  .chat-box {
    height: 400px;
    overflow-y: auto;
    background-color: #f8f9fa;
  }
  
  .message-bubble {
    max-width: 75%;
  }
  
  .text-left {
    text-align: left;
  }
  
  .text-right {
    text-align: right;
  }
  </style>
  