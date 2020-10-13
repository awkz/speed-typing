<template>
  <div class="game">
    <h2 v-bind:style="{ color: activeColor }">{{ word }}</h2>
    <input
      v-model="gameinput"
      v-on:keyup.enter="entered()"
      placeholder="type here"
    />
    <h3 v-bind:style="{ color: activeColor }">{{ status }}</h3>
  </div>
</template>

<script>
import Vue from 'vue';
import VueConfetti from 'vue-confetti'
Vue.use(VueConfetti)

let list = ['MAKAN','MINUM','AYAM GORENG', "KOPI SUSU", "MENGGALI"]
let order = 0
let totalOrders = list.length
export default {
  name: "Game",
  props: {
    appName: String,
  },
  mounted() {
    this.show()
  },
  data: function () {
    return {
      word: "",
      status: "",
      gameinput: "",
      activeColor: "black",
    };
  },
  methods:{
    entered(){
      if(this.word.toUpperCase() == this.gameinput.toUpperCase()){
        this.correct()
        if(totalOrders==order){
          this.status = "You Win"
          this.word = ""
          this.$confetti.start();
        } else {
          this.show()
        }
      } else{
        this.wrong()
      }
    },
    show(){
      this.word = list[order]
      this.activeColor = "black"
    },
    correct() {
      this.status = "CORRECT"
      this.activeColor = "green"
      this.gameinput= ""
      order += 1
    },
    wrong() {
      this.status = "WRONG"
      this.activeColor = "red"
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  width: 80%;
  background: transparent;
  text-align: center;
  font-size: 1.3em;
  font-weight: bold;
  outline: none;
  border: none;
  border-bottom: 1px solid black;
  text-transform: uppercase;
}
</style>
