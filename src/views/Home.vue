<template>
  <div class="home">
    <Login />
  </div>
</template>

<script>
import Login from '@/components/Login.vue'

export default {
  name: 'Home',
  components: {
    Login
  }
}
</script>

<style scoped>

.home {
  height: 100%;
  width: 100%;
  overflow-y: scroll;
  background-color: #06032b;
}

</style>