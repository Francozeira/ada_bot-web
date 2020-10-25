<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style>
body {
  margin: 0 !important;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: goldenrod;
  height: 100vh;
}

/* SCROLL */
/* width */
::-webkit-scrollbar {
  width: 5px;
}
/* Track */
::-webkit-scrollbar-track {
  background: transparent;
}
 
/* Handle */
::-webkit-scrollbar-thumb {
  background: rgba(255, 255, 0, 0.6); 
  border-radius: 10px;
}
/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: rgb(62, 66, 1); 
}

</style>
