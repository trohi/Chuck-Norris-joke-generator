<template>
  <div id="app">
  <img v-bind:src="img"> 
    <Joker v-bind:joke="joke"/>
    <button @click="generate">Generate new joke</button>
  </div>
</template>

<script>
import axios from "axios"
import Joker from './components/Joker.vue'
import { stringify } from 'querystring';

export default {
  name: 'app',
  components: {
    Joker
  },
  data(){
    return{
      joke:"",
      img:""
    }
  },
  methods:{
    generate(){
      axios.get("https://api.chucknorris.io/jokes/random")
    .then(res=>{
      stringify(res)
      //eslint-disable-next-line
      console.log(res)
      this.joke = res.data.value
      this.img = res.data.icon_url
    })
    }
  },
  created(){
    axios.get("https://api.chucknorris.io/jokes/random")
    .then(res=>{
      stringify(res)
      //eslint-disable-next-line
      console.log(res)
      this.joke = res.data.value
      this.img = res.data.icon_url
    })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
