<template>
  <div class="noIdReturn">
    <div class="warningContainer">
      <div class="txtLg">Oooops</div>
      <div>
        <i class="fas fa-users-slash fa-7x"></i>
        <div class="txtDesc" >Parece que você ainda não preencheu sua matrícula ou identificação</div>
        <div class="txtDesc" >Por favor, retorne a página de login</div>
      </div>

      <router-link to="/" tag="button" class="returnHome">
        <div><i class="fas fa-undo"></i> Retornar</div>
      </router-link>

    </div>
  </div>
</template>

<script>

export default {
  name: 'noIdReturn',
  computed: {
    user () {
      return this.$store.state.user
    }
  }
}
</script>

<style scoped>

.noIdReturn {
  height: 100%;
  width: 100%;
  overflow-y: scroll;
  background:linear-gradient(rgba(0, 0, 0, 0.7),  rgba(0, 0, 0, .9)) 
}

.warningContainer {
  width: 60%;
  height: 300px;
  position: relative;
  margin: 10% auto;
  padding: 20px 50px;
  border-radius: 10px;
  background-color: #421515;
  color: aliceblue;
  font-family: 'Baloo Tamma 2', cursive;
}

.returnHome {
  width: 80%;
  max-width: 400px;
  height: 40px;
  position: absolute;
  bottom: 20px; 
  right: 30px;
  border-radius: 10px;
  cursor: pointer;
  padding: 0;
  font-family: 'Alata', sans-serif;
  font-size: 1.3em;
  border: currentColor;
  background-color: rgb(187, 4, 4);
  color: white;
}

/* ICONS */

.fa-users-slash {
  float: left;
  margin-right: 30px;
}

.fa-undo {
  margin-right: 10px;
}

/* FONTS */

.txtLg {
  margin-bottom: 30px;
  font-family: 'Alata', sans-serif;
  text-align: left;
  font-size: 3em;
}

.txtDesc {
  text-align: left;
  font-size: 1.5em;
}

/* MEDIA QUERIES */
@media only screen and (max-width: 560px) {

  .warningContainer {
    width: 60%;
    height: 80%;

  }
  
  /* ICONS */

  .fa-users-slash {
    margin-bottom: 50px;
  }

  /* FONTS */

  .txtLg {
    margin-bottom: 30px;
    font-family: 'Alata', sans-serif;
    text-align: left;
    font-size: 2em;
  }

  .txtDesc {
    margin-bottom: 20px;
    text-align: left;
    font-size: 1em;
  }
}
</style>