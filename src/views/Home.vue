<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <AdaContainer />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

// export default {
//   name: 'Home',
//   components: {
//     HelloWorld
//   }
// }
import AdaContainer from '@/components/AdaContainer.vue'

export default {
  name: 'Home',
  components: {
    AdaContainer
  }
}
</script>

<style scoped>

.home {
  height: 100%;
  width: 100%;
  background-image: url("../assets/home_print3.png");
  background-repeat: no-repeat;
  background-size: cover;
  display: flex;
}

/* MEDIA QUERIES */
@media only screen and (max-width: 560px) {

  .home {
    background-image: url("../assets/mobile_print1.jpg");
  }
}
</style>