<template>
  <div class="adaContainer">
    <img v-if="chatbotOpened === false" @click="chatbotOpened = true" class="ada-btn" src="../assets/ada_yellow cropped.png" alt="Ada">
    <div v-else class="chatContainer" @click="chatbotOpened = false">
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

.chatContainer {
  position: absolute;
  bottom: 0px;
  right: 0px;
  width: 500px;
  height: 500px;
  background-color: cyan;
}

.ada-btn {
  border-radius: 50%;
  width: 250px;
  height: 250px;
}

.ada-btn:hover {
  cursor: pointer;
  /* filter: blur(2px); COLL TO ADD TO BACKGROUND*/
  filter: contrast(150%) drop-shadow(8px 8px 10px rgb(255, 251, 1));
  filter: saturate(2) drop-shadow(8px 8px 10px rgb(255, 251, 1));
}
</style>
