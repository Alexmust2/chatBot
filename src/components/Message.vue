<template>
    <div :class="[message.type === 'user' ? 'user-message message' : 'bot-message message']">
      <div class="avatar" :class="message.type"></div>
      <div class="message-content">
        <div class="message-avatar" :class="message.type"></div>
        <span class="message-text" v-html="formatMessage(message.text)"></span>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['message'],
    methods: {
      formatMessage(text) {
        return text.replace(/\n/g, '<br>');
      },
    },
  };
  </script>

  <style>
.message {
  display: flex;
  flex-direction: column;
  padding: 10px;
  border-radius: 18px;
  max-width: 70%;
  min-width: 120px;
  word-wrap: break-word;
  margin-bottom: 5px;
  position: relative;
}

.user-message {
  background-color: #007bff;
  color: #fff;
  align-self: flex-end;
}

.bot-message {
  background-color: #f4f4f4;
  color: #000;
  align-self: flex-start;
}

.message-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}

.message-avatar {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  position: absolute;
  top: -45px;
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
}

.message-avatar.user {
  background-color: #007bff;
  background-image: url('@/assets/user-avatar.jpg');
  right: 0;
}

.message-avatar.bot {
  background-color: #f4f4f4;
  background-image: url('@/assets/bot-avatar.png');
  left: 0;
}

.message-text {
  z-index: 1;
}


</style>
  