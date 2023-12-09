<template>
  <div class="chat-container">
    <MessageContainer :messages="messages" />
    <Options ref="options" :options="options" @sendMessage="handleSendMessage" />
    <InputContainer :value="newMessage" @update:value="updateNewMessage" @sendMessage="sendMessage" />
  </div>
</template>

<script>
import MessageContainer from './MessageContainer.vue';
import questions from '@/data/questions.json'
import Options from './Options.vue';
import InputContainer from './InputContainer.vue';

export default {
  data() {
    return {
      messages: [],
      questions: [],
      options: [],
      newMessage: '',
      answering: false
    };
  },
  mounted() {
  this.questions = questions;
  this.loadOptions();
  this.messages.push({ type: 'bot', text: 'Привет! Что я могу для Вас сделать?' });
},
  methods: {
    updateNewMessage(value) {
      this.newMessage = value;
    },
    handleSendMessage(optionText) {
      this.sendMessage(optionText)
    },
    loadOptions() {
      let optionsLength = 0;
      for (optionsLength; optionsLength < 3; optionsLength += 1) {
        this.options.push({ text: this.questions[optionsLength].question });
      }
    },
    sendMessage(value) {
      if(!this.answering){
        this.answering = true
        let text = value.toLowerCase();
        if (text === 'список вопросов') {
          this.messages.push({ type: 'user', text: value });
          const questionList = this.questions.slice(3).map((q, index) => `${index + 1}. ${q.question}`).join('<br>');
          setTimeout(() => {
            this.messages.push({ type: 'bot', text: questionList });
            this.answering = false
          }, 500);
        } else {
          const question = this.questions.find((q) => q.question.toLowerCase().includes(text.toLowerCase()));
          if (question) {
            this.messages.push({ type: 'user', text: value });
            setTimeout(() => {
              this.messages.push({ type: 'bot', text: question.answer });
            this.answering = false

            }, 500);
          } else {
            this.messages.push({ type: 'user', text: value });
            setTimeout(() => {
              this.messages.push({ type: 'bot', text: 'Извините, я не понимаю. Попробуйте перефразировать.' });
            this.answering = false
            }, 500);
          }
        }
        this.newMessage = '';
        setTimeout(() => {
          this.$nextTick(() => {
            const optionsComponent = this.$refs.options;
            const lastOption = optionsComponent.$el.children[optionsComponent.$el.children.length - 1];
            if (lastOption) {
              lastOption.scrollIntoView({ behavior: "smooth", block: "end" });
            }
          });
        }, 500);
      }
    },
  },
  components: {
  MessageContainer,
  Options,
  InputContainer,
},
};
</script>

<style>
.chat-container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 20px;
  background-color: #8a2be2;
  height: 100vh;
  overflow-y: auto;
}
</style>