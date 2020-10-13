<template>
  <div class="game">
    <h2 v-bind:style="{ color: activeColor }">{{ word }}</h2>
    <input v-model="gameinput" v-on:keyup.enter="entered()" placeholder="type here" />
    <h3>{{ status }}</h3>
  </div>
</template>

<script>
export default {
  name: "Game",
  props: {
    appName: String,
  },
  data: function () {
    return {
      list: ['MAKAN','MINUM',''],
      word: "MAKAN",
      status: "",
      gameinput: "",
      activeColor: "black",
    };
  },
  methods:{
    entered(){
      if(this.word.toUpperCase() == this.gameinput.toUpperCase()){
        this.status = "CORRECT";
        this.activeColor = "green";
        this.gameinput= "";
      } else{
        this.status = "WRONG";
        this.activeColor = "red";
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input{
    width:100%;
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
