<template>
    <div class="message-container" v-for="(message, index) in messages" :key="index">
      <Message :message="message" />
    </div>
  </template>
  
  <script>
  import Message from './Message.vue';
  
  export default {
    props: ['messages'],
    components: {
      Message,
    },
  };
  </script>

  <style>
.message-container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 10px;
  margin-top: 25px;
  width: 100%;
}

</style>
  