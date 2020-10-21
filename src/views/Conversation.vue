<template>
  <div class="conversation">
    <NoIdReturn  v-if="this.user === null"/>
    <AdaContainer  v-else />
  </div>
</template>

<script>
import AdaContainer from '@/components/AdaContainer.vue'
import NoIdReturn from '@/components/NoIdReturn.vue'

export default {
  name: 'Home',
  components: {
    AdaContainer, NoIdReturn
  },
  computed: {
    user () {
      return this.$store.state.user
    }
  },
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
