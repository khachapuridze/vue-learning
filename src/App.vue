<template>
  <div id="app">
    <Header 
      v-if="questions.length"
      :qurrentQuestion="questions[index]"
      :questions = questions
      :index = index
      :countcorrect = countcorrect
    />
    <b-container class="bv-example-row">
  <b-row>
    <b-col sm="6" offset="3">
      <Questionbox 
      v-if="questions.length"
      :qurrentQuestion="questions[index]"
      :next="next"
      :prev="prev"
      />
    </b-col>
  </b-row>
</b-container>

  </div>
</template>

<script>

import Header from "./components/Header.vue"
import Questionbox from "./components/Questionbox.vue"

export default {
  name: 'app',
  components: {
    Header,
    Questionbox
  },
  data() {
    return {
      questions: [],
      index: 0
    }
  },
  methods: {
    next() {
      this.index++
    },
    prev() {
      this.index--
    }

  }
  ,
  mounted() {
    fetch("https://opentdb.com/api.php?amount=10&category=17&difficulty=easy&type=multiple", {
      method: 'get'
    }).then ((resp)=> {
      return resp.json();
    }).then((final) =>{
      this.questions = final.results;
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
