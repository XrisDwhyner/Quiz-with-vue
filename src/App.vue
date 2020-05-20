<template>
  <div id="app">
    <Header
    :numCorrect = "numCorrect"
    :numTotal = "numTotal"
    />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
          v-if="questions.length"
          :currentQuestion="questions[index]"
          :next="next"
          :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'


export default {
  name: 'App',
  components: {
    Header,
    QuestionBox
  },
  data(){
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0
    }
  },
  methods:{
    next(){
      this.index++;
    },
    increment(isCorrect){
      if (isCorrect){
        this.numCorrect++
      }
      this.numTotal++
    }
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=20&type=multiple', {
      method: 'get'
    })
    .then((response)=>{
      return response.json()
    })
    .then((jsonData)=>{
      this.questions = jsonData.results
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
img {
  width: 150px;
  border-radius: 2px;
  box-shadow: 1px 1px 3px 1px rgba(0, 0, 0, 0.5);
  transition: width 1s;
}
img:hover {
  cursor: pointer;
}

</style>
