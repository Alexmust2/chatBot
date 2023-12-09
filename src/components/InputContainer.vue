<template>
    <div class="input-container">
      <input :value="value" @input="handleInput" class="form-control" placeholder="Type your message..."  @keyup.enter="sendMessageChildren(value)"/>
      <button @click="sendMessageChildren(value)" class="btn btn-primary send-button"></button>
    </div>
  </template>
  
  <script>
  export default {
    props: ['value', 'sendMessage'],
    methods: {
      handleInput(event) {
        this.$emit('update:value', event.target.value);
      },
      sendMessageChildren(value) {
        this.$emit('sendMessage', value);
      },
    },
  };
  </script>
  

<style>

.input-container {
  position: fixed;
  bottom: 0;
  width: 100%;
  height: 50px;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #fff;
  padding: 0 10px;
  box-shadow: 0px -2px 5px rgba(0, 0, 0, 0.1);
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
  z-index: 1;
}

.form-control {
  flex: 1;
  outline: none;
  height: 100%;
  padding: 10px 15px;
  border: none;
  border-bottom-left-radius: 15px;
  border-top-left-radius: 15px;
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}

.send-button {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 30px;
  top: 5px;
  border-radius: 50%;
  color: #fff;
  border: none;
  cursor: pointer;
  position: relative;
  background-image: url('@/assets/paper-plane.png');
  background-size: contain;
  background-repeat: no-repeat;
  transform: rotate(45deg);
}

</style>