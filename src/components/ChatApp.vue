<template>
  <div class="hello container">
    <div v-if = "!gameStarted">
      <div v-if="msg != ''" class="notification is-danger">
        <button @click='deleteMsg' class="delete"></button>
        {{ msg }}
      </div>
      <nav class="panel">
        <p class="panel-heading has-text-primary">
          Game Name
        </p>
        <div class="panel-block is-size-4-desktop is-flex">
          <div class="container">
            <div class="field is-grouped is-grouped-centered">
              <h6>You'r gender is :</h6>
              <p class="control">
                <button @click='genders' v-bind:class="{ 'is-outlined' : gender =='Female','is-active' : gender =='Male'}" value="Male" class="button is-info is-rounded">Male</button>
              </p>
              <p class="control">
                <button @click='genders'  v-bind:class="{ 'is-outlined' : gender =='Male','is-active' : gender =='Female'}" value="Female" class="button is-danger is-rounded">Female</button>
              </p>
            </div>
          </div>
        </div>
        <div class="panel-block">
          <div class="container">
            <div class="field is-grouped is-grouped-centered">
              <p class="control">
                <label>Cr*** Name:</label>
              </p>
              <p class="control">
                <input @keyup="getName" class="input" type="text" required>
              </p>
            </div>
          </div>
        </div>
        <div class="panel-block">
          <button @click='startGame' class="button is-link is-outlined is-rounded is-fullwidth">
            Start Game
          </button>
        </div>
      </nav>
    </div>

    <div v-else>
      <div v-if="msg == 'Male'">
        <Male v-bind:name="name"/>
      </div>
      <div v-else-if="msg == 'Female'">
        <Female v-bind:name="name"/>
      </div>
    </div>
  </div>
</template>

<script>
import Male from './Male.vue';
import Female from './Female.vue';

export default {
  name: 'HelloWorld',
  components: {
    Male,
    Female
  },
  props: {},
  data() {
    return {
      gender : '',
      name : '',
      msg : '',
      gameStarted : false
    }
  },
  methods : {
    genders(e) {
      this.gender = e.target.value;
    },
    getName(e) {
      this.name = e.target.value;
    },
    startGame() {
      if (this.name == '') {
        this.msg = 'Enter Name !';
      } else if (this.gender == '') {
        this.msg = 'Select Gender !';
      } else {
        this.msg = this.gender ;
        this.gameStarted = true ;
      }
    },
    deleteMsg(){
      this.msg = '';
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
