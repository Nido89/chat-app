<template>
  <div class="chat-window">
    <div class="messages">
      <div class="message" v-for="message in messages" v-bind:key="message._id">
        <div class="username">{{message.username}}</div>
        <div class="message-text">{{message.msg}}</div>
      </div>
    </div>
    <form class="input-container" v-on:submit="sendMessage">
      <input type="text" v-model="msg" />
      <button v-on:click="sendMessage" v-bind:disabled="!msg">SEND</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "chatroom",
  props: ["messages"],
  data: function() {
    return {
      msg: ""
    };
  },
  methods: {
    sendMessage: function() {
      if (!this.msg) {
        alert("Please enter a message");
        return;
      }
      this.$emit("sendMessage", this.msg);
      this.msg = "";
    }
  }
};
</script>

<style lang="scss" scoped>
.chat-window {
  flex: 1;
  display: flex;
  flex-direction: column;
  background-color: rgb(52, 164, 255);
  color: #000000;
  box-shadow: 1px 1px 6px 0px rgba($color: #000000, $alpha: 0.15);
  .messages {
    flex: 1;
    overflow: scroll;
    background-color: khaki;
    .message {
      display: flex;
      border-bottom: royalblue;
      padding: 10px;
      color: rgb(0, 133, 126);
      background-color: rgb(110, 110, 110);

      &:last-of-type {
        border-bottom: rgb(255, 0, 0);
      }
      .username {
        color: rgb(37, 129, 0);
        width: 100px;
        margin-right: 15px;
        background-color: rgb(239, 199, 255);
      }
      .message-text {
        flex: 1;
        background-color: rgb(255, 172, 133);
        color: rgb(2, 39, 202);
      }
    }
  }
  .input-container {
    display: flex;
    input {
      flex: 1;
      height: 35px;
      font-size: 18px;
      box-sizing: border-box;
    }
    button {
      width: 75px;
      height: 35px;
      box-sizing: border-box;
    }
  }
}
</style>