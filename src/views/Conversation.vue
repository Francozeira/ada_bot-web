<template>
  <div class="conversation">
    <AdaContainer />
  </div>
</template>

<script>
import AdaContainer from '@/components/AdaContainer.vue'

export default {
  name: 'Home',
  components: {
    AdaContainer
  }
}
</script>

<style scoped>

.conversation {
  height: 100%;
  width: 100%;
  background-image: url("../assets/web_1.png");
  background-repeat: no-repeat;
  background-size: cover;
  display: flex;
}

</style>
