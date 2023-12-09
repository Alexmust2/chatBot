<template>
    <div class="options">
      <button v-for="option in options" :key="option.text" @click="handleClick(option.text)" class="chat-option">
        {{ option.text }}
      </button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['options', 'sendMessage'],
    methods: {
      handleClick(optionText) {
        this.$emit('sendMessage', optionText);
      }
    }
  };
  </script>

  <style>

.options {
  display: flex;
  flex-wrap: wrap;
  max-width: 40%;
  justify-content: flex-start;
  margin-bottom: 35px;
}


.chat-option {
  margin: 5px;
  padding: 10px 20px;
  border: none;
  border-radius: 20px;
  background-color: #fff;
  cursor: pointer;
}

.chat-option:hover {
  background-color: #aa66eb;
  color: #fff;
}

</style>
  