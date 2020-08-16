<template>
  <div class="adaContainer">
    <img v-if="chatbotOpened === false" @click="chatbotOpened = true" class="ada-btn" src="../assets/ada_yellow cropped.png" alt="Ada">
    <div v-else class="chatContainer">

      <div class="containerHeader">
          <img class="adaChatLogo" src="../assets/ada_yellow cropped.png" alt="Ada">
          <div class="adaChatTitle">
            <span class="status"></span>
            Ada Chatbot
            <span class="adaChatInfo">Online</span>
          </div>
          <div class="adaHeaderIcons">
            <div @click="chatbotOpened = false" class="closeChatBtn">
              <i class=" fas fa-times"></i>
            </div>
            <div @click="chatbotOpened = false" class="bugChatBtn">
              <i class="fas fa-bug"></i>
            </div>
          </div>
      </div>

      <div class="containerBody">

      </div>

      <div class="containerFooter">

      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'AdaContainer',
  props: {
    // msg: String
  },
  data: function () {
  return {
    chatbotOpened: false
  }
}
}
</script>

<style scoped>

.adaContainer {
  position: absolute;
  bottom: 30px;
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
  background-color: rgb(94, 0, 0);
  color: aliceblue;
  font-size: 1.5em;
  width: 50px;
  height: fit-content;
  border-radius: 5px;
  padding: 5px 0;
}

.closeChatBtn:hover {
  cursor: pointer;
  background-color: rgb(255, 0, 0);
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
  width: 98%;
  height: 305px;
	display: flex;
  margin: 5px auto;
  border-radius: 5px;
  background-color: aliceblue;
}

.containerFooter {
  width: 98%;
  height: 100px;
  bottom: 0;  
  margin: auto;
  border-radius: 5px;
  background-color: cornflowerblue;
}

/* MEDIA QUERIES */
@media only screen and (max-width: 500px) {
  
}
</style>
