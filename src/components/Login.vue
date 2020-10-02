<template>
  <div class="login">
      <div class="txtLg">Ada Bot</div>
      <!-- <img src="../assets/ada.jpg" alt=""> -->

    <div class="formContainer">
      <div class="txtLg">Usuário:</div>
      <div>Selecione entre Aluno e insira sua matrícula ou entre como visitante para que eu possa começar o seu atendimento</div>
        <div class="optContainer">
          <div @click="optStudent" :class="this.option === 'student' ? 'optSelected' : 'notSelected'" class="studentOpt">
            <i class="optIcon fas fa-user-graduate fa-7x"></i>
            <div class="optTxt">Aluno</div>
          </div>
          <div @click="optGuest" :class="this.option === 'guest' ? 'optSelected' : 'notSelected'" class="guestOpt">
            <i class="optIcon fas fa-user fa-7x"></i>
            <div class="optTxt">Visitante</div>
          </div>
        </div>

      <router-link to="/conversation" tag="button" :disabled="user === null" class="enterConversation">
        <div v-if="user === null" class="">Selecione o Usuário <i class="far fa-times-circle"></i></div>
        <div v-else class="">Acessar portal <i class="fas fa-sign-in-alt"></i></div>
      </router-link>

      <div>{{this.$store.state.user}}</div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'login',
  data: function () {
    return {
      option: ''
    }
  },
  computed: {
    user () {
      return this.$store.state.user
    }
  },
  methods: {
    optGuest () {
      if(this.option !== 'guest') {
        this.option = 'guest'
        const user_id = Math.floor(Math.random() * 100000000).toString().padStart(8, '0')
        this.$store.commit('upateUser', user_id)
      }
    },
    optStudent () {
      this.option = 'student'
      console.log(Math.floor(Math.random() * 1000000000));
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.formContainer {
  height: 500px;
  width: 80%;
  max-width: 700px;
  margin: 0 auto;
  border-radius: 10px;
  background-color: #152642;
  color: aliceblue;
  font-family: 'Baloo Tamma 2', cursive;
}

.txtLg {
  font-size: 2em;
  font-family: 'Alata', sans-serif;
}

.enterConversation {
  width: 80%;
  max-width: 400px;
  height: 40px;
  margin-left: 10px;
  border-radius: 10px;
  cursor: pointer;
  padding: 0;
  border: currentColor;
  background-color: rgb(0, 151, 68);
  color: white;
}

.enterConversation:disabled {
  cursor: not-allowed;
  background-color: rgba(0, 151, 68, 0.2);
  color: rgba(255, 255, 255, 0.2);
}

.optContainer {
  width: 100%;
  display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	justify-content: center;
	align-items: stretch;
	align-content: stretch;
}

.studentOpt {
  width: 50%;
  height: 200px;
  border-radius: 20px;
  margin: 40px 20px 40px 40px;
  cursor: pointer;
  background-color: rgba(255, 166, 0, 0.9);
}

.regStudent {
  border: 20px solid rgba(94, 93, 93, 0.61);
  color:  rgba(255, 255, 255, 0.5);
}

.guestOpt {
  width: 50%;
  height: 200px;
  border-radius: 20px;
  margin: 40px 40px 40px 20px;
  cursor: pointer;
  background-color: rgba(124, 0, 128, 0.9);
}

.notSelected {
  border: 20px solid rgba(94, 93, 93, 0.61);
  color:  rgba(255, 255, 255, 0.5);
}


.optSelected {
  border: 20px solid rgba(255, 255, 255, 1) ;
  color: 20px solid rgba(255, 255, 255, 1);
}

.optIcon {
  margin-top: 20px;
}

.optTxt {
  margin-top: 20px;
}

/* MEDIA QUERIES */
@media only screen and (max-width: 560px) {

  .formContainer {
    width: 95vw;
  }
}

</style>
