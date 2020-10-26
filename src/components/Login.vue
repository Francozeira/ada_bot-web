<template>
  <div class="login">
    <div class="HeaderTxt">    
      <img class="ada-btn" src="../assets/ada_yellow cropped.png" alt="">
      Ada Bot
    </div>

    <div class="formContainer">
      <div class="txtLg">Usuário</div>
      <div class="descriptionTxt">Selecione entre Aluno e insira sua matrícula ou entre como visitante para que eu possa começar o seu atendimento</div>
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

      <div v-if="this.option === 'guest'">
        Entrando com ID gerado automaticamente:
        <span class="txtAlt">{{this.user}}</span>
      </div>

      <div v-if="this.option === 'student'">
        Digite sua Matrícula (8 dígitos apenas):
        <input type="number" @input="validateInput($event)" :value="student_id" ref="registry" class="registry">
      </div>

      <router-link to="/conversation" tag="button" :disabled="user === null" class="enterConversation">
        <div v-if="user === null" class="">Selecione o Usuário <i class="far fa-times-circle"></i></div>
        <div v-else class="">Acessar portal <i class="fas fa-sign-in-alt"></i></div>
      </router-link>

    </div>

  </div>
</template>

<script>
export default {
  name: 'login',
  data: function () {
    return {
      option: '',
      student_id: ''
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
      this.$store.commit('upateUser', null)
      this.option = 'student'
    },
    validateInput: function() {
      if (this.$refs.registry.value.length > 8) {
        this.$refs.registry.value = this.student_id
      } else this.student_id = this.$refs.registry.value
    }
  },
  watch: {
    student_id: function () {
      if (this.student_id.length === 8) this.$store.commit('upateUser', this.student_id)
      if (this.user != null && this.student_id.length < 8) this.$store.commit('upateUser', null)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type=number] {
  -moz-appearance: textfield;
}


.ada-btn {
  vertical-align: text-bottom;
  border-radius: 50%;
  width: 100px;
  height: 100px;
}

.ada-btn:hover {
  cursor: pointer;
  filter: contrast(150%) drop-shadow(4px 4px 5px rgb(255, 251, 1));
  filter: saturate(2) drop-shadow(4px 4px 5px rgb(255, 251, 1));
}

.formContainer {
  width: 80%;
  max-width: 700px;
  margin: 0 auto 50px auto;
  padding-top: 30px;
  border-radius: 10px;
  background-color: #152642;
  color: aliceblue;
  font-family: 'Baloo Tamma 2', cursive;
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

.registry {
  width: 92px;
  font-size: 1.2em;
  font-family: 'Alata', sans-serif;
  font-weight: bold;
  padding: 5px 10px;
  margin-left: 10px;
  border: none;
  border-radius: 10px;
  outline: none;
  -webkit-appearance: none;
  background-color: rgb(0, 0, 0, 0.2);
  color: white;
}

.enterConversation {
  width: 80%;
  max-width: 400px;
  height: 40px;
  margin: 20px 0 40px 0;
  border-radius: 10px;
  cursor: pointer;
  padding: 0;
  font-size: 1.3em;
  border: currentColor;
  background-color: rgb(0, 151, 68);
  color: white;
}

/* FONTS */

.HeaderTxt {
  margin: 50px auto 40px auto;
  font-family: 'Alata', sans-serif;
  font-size: 3em;
  font-weight: 600;
  color:yellow;
}

.txtLg {
  margin: 0 20px 0 20px;
  font-family: 'Alata', sans-serif;
  text-align: left;
  font-size: 2em;
  color:yellow;
}

.descriptionTxt {
  margin: 20px;
  text-align: justify;
}

.txtAlt {
  font-size: 1.2em;
  font-family: 'Alata', sans-serif;
  font-weight: bold;
  border-radius: 10px;
  padding: 5px 10px;
  margin-left: 10px;
  background-color: rgb(0, 0, 0, 0.2);
}
/* MEDIA QUERIES */
@media only screen and (max-width: 560px) {

  .formContainer {
    width: 95vw;
  }

  .studentOpt {
    width: 50%;
    height: 200px;
    border-radius: 20px;
    margin: 40px 10px 20px 20px;
    cursor: pointer;
    background-color: rgba(255, 166, 0, 0.9);
  }

  .guestOpt {
    width: 50%;
    height: 200px;
    border-radius: 20px;
    margin: 40px 20px 20px 10px;
    cursor: pointer;
    background-color: rgba(124, 0, 128, 0.9);
  }

  .notSelected {
    border: 10px solid rgba(94, 93, 93, 0.61);
    color:  rgba(255, 255, 255, 0.5);
  }

  .optSelected {
    border: 10px solid rgba(255, 255, 255, 1) ;
    color:  rgba(255, 255, 255, 1);
  }

  .registry {
    width: 102px;
  }

}

</style>