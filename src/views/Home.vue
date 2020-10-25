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
  background: rgb(2,9,122);
  background: linear-gradient(125deg, rgba(2,9,122,1) 0%, rgba(3,125,121,1) 50%, rgba(6,0,48,1) 100%);
}

</style>