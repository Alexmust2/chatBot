<template>
  <div id="app">
    <ChatContainer />
  </div>
</template>

<script>
import ChatContainer from "./components/ChatContainer.vue";

export default {
  name: "App",
  components: {
    ChatContainer
},
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>