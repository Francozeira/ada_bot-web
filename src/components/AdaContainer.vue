<template>
  <div class="adaContainer">
    <img v-if="chatbotOpened === false" @click="chatbotOpened = true" class="ada-btn" src="../assets/ada_yellow cropped.png" alt="Ada">
    <div v-else class="chatContainer">

      <div class="containerHeader">
          <img class="adaChatLogo" src="../assets/ada_yellow cropped.png" alt="Ada">
          <div class="adaChatTitle">
            <span class="status"></span>
            Ada Chatbot
            <span class="adaChatInfo">ID: {{this.user}}</span>
          </div>
          <div class="adaHeaderIcons">
            <div @click="chatbotOpened = false" class="closeChatBtn">
              <i class="fas fa-minus"></i>
            </div>
            <!-- <div @click="chatbotOpened = false" class="bugChatBtn">
              <i class="fas fa-bug"></i>
            </div> -->
          </div>
      </div>

      <div class="containerBody" id="containerBody">

        <div v-for="msg in sessionMessages" :key="msg.msgId" class="msgContainer">
          <div class="msgBubble" v-bind:class="{ userMsg: msg.origin === 'user',  botMsg: msg.origin === 'bot'}">

            <!-- IN CASE OF BOT MESSAGE, USE SUPPLIED WATSON TEXT -->
            <div v-if="msg.origin === 'bot'" v-html="msg.text" ></div>
            <div v-else >{{msg.text}}</div>

          </div>
          
        </div>

      </div>

      <div class="containerFooter">
        <input type="text" class="botInput" v-on:keyup="checkInput" v-model="msg" placeholder="Digite uma mensagem...">
        <button class="sendMsg" @click='sendInput'><i class="fas fa-paper-plane"></i></button>
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'AdaContainer',
  props: {
    // msg: String
  },
  data: function () {
    return {
      chatbotOpened: false,
      msg: '',
      sessionMessages: []
    }
  },
  computed: {
    user () {
      return this.$store.state.user
    }
  },
  methods: {

    // TREATING THE CASE OF USER PRESSES ENTER
    checkInput(e) {
      if (e.keyCode === 13 && this.msg !== '') {
        this.sendInput()
      }
    },

    // SEND TYPED TEXT TO BACKEND SERVICE
    sendInput() {
      
      if (this.msg !== '') {
        this.sessionMessages.push({
          origin: 'user',
          text: this.msg,
          msgId: this.sessionMessages.length + 1
          })

        axios.post('https://ada-bot.mybluemix.net/api/messages', {
          "user_id": this.user,
          "type": "text",
          "text": this.msg
        })

        .then((response) => {
          console.log(response.data)
          this.sessionMessages.push({
            origin: 'bot',
            text: response.data.message,
            msgId: this.sessionMessages.length + 1
          })
        })

        this.msg = ''
        this.scrollDownMessages()
      }
    },
    
    // SCROLL DOWN MESSAGES DIV
    scrollDownMessages() {
      setTimeout(() => {
        const el = document.getElementById("containerBody")
        el.scrollTop = el.scrollHeight
      }, 2000)
    }

  },
}
</script>

<style scoped>

*:focus {
  outline: none;
}

a {
  text-decoration: none;
  color: #FFFFFF;
}

.adaContainer {
  position: absolute;
  bottom: 20px;
  right: 30px;
}

.ada-btn {
  border-radius: 50%;
  width: 100px;
  height: 100px;
}

.ada-btn:hover {
  cursor: pointer;
  filter: contrast(150%) drop-shadow(8px 8px 10px rgb(255, 251, 1));
  filter: saturate(2) drop-shadow(8px 8px 10px rgb(255, 251, 1));
}

.chatContainer {
  position: absolute;
  bottom: 0px;
  right: 0px;
  width: 500px;
  height: 500px;
  background-color: rgba(19, 20, 0);
  border-radius: 5px;
}

.containerHeader {
  width: 100%;
  height: 80px;
	display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	justify-content: flex-start;
	align-items: center;
	align-content: stretch;
}

.adaChatLogo {
  width: 70px;
  height: 70px;
  border-radius: 50%;
  margin: 5px 0 0 10px;
}

.adaChatTitle {
  position: relative;
  font-family: 'Alata', sans-serif;
  color: white;
  font-size: 1.5em;
  padding-left: 10px;
}

.adaChatInfo {
  position: absolute;
  bottom: -25px;
  left: 25px;
  font-family: 'Baloo Tamma 2', cursive;
  color: darkslategray;
  font-size: 0.8em;
}

.status {
  height: 10px;
  width: 10px;
  background-color: rgb(46, 197, 8);
  border-radius: 50%;
  display: inline-block;
  margin-bottom: 3px;
}

.adaHeaderIcons {
  position: absolute;
  top: 0px;
  right: 0px;
  width: 200px;
  display: flex;
	flex-direction: row-reverse;
	flex-wrap: nowrap;
	justify-content: flex-start;
	align-items: stretch;
	align-content: stretch;
}

.closeChatBtn {
  /* background-color: rgb(94, 0, 0);
   */
  background-color: rgb(94, 88, 0);
  color: aliceblue;
  font-size: 1.5em;
  width: 50px;
  height: fit-content;
  border-radius: 5px;
  padding: 5px 0;
}

.closeChatBtn:hover {
  cursor: pointer;
  /* background-color: rgb(255, 0, 0); */
  background-color: rgb(214, 200, 3);
}

.bugChatBtn {
  background-color: rgb(94, 88, 0);
  color: aliceblue;
  font-size: 1.5em;
  width: 50px;
  height: fit-content;
  border-radius: 5px;
  padding: 5px 0;
}

.bugChatBtn:hover {
  cursor: pointer;
  background-color: rgb(214, 200, 3);
}

.containerBody {
  width: 95%;
  height: 345px;
  overflow-y: auto;
  display: flex;
  flex-flow: column nowrap;
  margin: 5px auto;
  border-radius: 5px;
  background-color: rgb(32, 34, 0);
  /* align-items: flex-start; */
}

.containerBody > :first-child {
  margin-top: auto !important;
  /* use !important to prevent breakage from child margin settings */
}

.containerFooter {
  width: 95%;
  height: 40px;
  margin: 15px auto 0 auto;
  border-radius: 5px;
  display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	justify-content: flex-start;
	align-items: stretch;
	align-content: stretch;
}

.botInput {
  width: calc(100% - 40px);
  border-radius: 15px;
  padding: 10px 15px;
  border: currentColor;
  background-color: rgb(62, 66, 1);
  color: white;
}

.sendMsg {
  width: 40px;
  margin-left: 10px;
  border-radius: 100%;
  cursor: pointer;
  padding: 0;
  border: currentColor;
  background-color: rgb(0, 151, 68);
  color: white;
}

.sendMsg:hover, .sendMsg:focus {
  border: currentColor;
  background-color: rgb(1, 255, 115);
}

.fa-paper-plane {
  font-size: 1.5em;
}

.msgBubble {
	position: relative;
  width: fit-content;
  min-width: 50px;
  max-width: 75%;
  min-height: 35px;
  margin: 15px;
  padding: 5px 15px;
	border-radius: .4em;
  color: white;
  text-align: left;
}

.userMsg {
  margin-left: auto; 
  margin-right: 15px;
  background-color: rgb(1, 112, 50);
}

.userMsg:after {
	content: '';
	position: absolute;
  right: 0;
	top: 25px;
	width: 0;
	height: 0;
	border: 22px solid transparent;
	border-left-color: rgb(1, 112, 50);
	border-right: 0;
	margin-top: -25px;
	margin-right: -11px;
}

.botMsg {
  background: rgb(19, 20, 0);
  color: white;
  overflow-wrap: break-word;
}

.botMsg:after {
	content: '';
	position: absolute;
	left: 0;
	top: 25px;
	width: 0;
	height: 0;
	border: 22px solid transparent;
	border-right-color: rgb(19, 20, 0);
	border-left: 0;
	margin-top: -25px;
	margin-left: -11px;
}

/* SCROLL */
/* width */
::-webkit-scrollbar {
  width: 5px;
}
/* Track */
::-webkit-scrollbar-track {
  background: black;
}
 
/* Handle */
::-webkit-scrollbar-thumb {
  background: rgb(255, 255, 255); 
  border-radius: 10px;
}
/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: rgb(62, 66, 1); 
}

/* MEDIA QUERIES */
@media only screen and (max-width: 560px) {
  .adaContainer {
    position: absolute;
    right: 2.5vw;
    bottom: 10px;
  }

  .chatContainer {
    width: 95vw;
  }
}
</style>