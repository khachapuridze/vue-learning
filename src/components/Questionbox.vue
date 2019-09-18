<template>
<div>
  <b-jumbotron >

    <template slot="lead">
        {{qurrentQuestion.question}}
    </template>

    <hr class="my-4">

    <b-list-group>
      <b-list-group-item  
      @click.prevent="select(index)" 
      v-bind:class="submited(index)"
       v-bind:key="index" v-for="(ans,index) in answers">{{ans}}</b-list-group-item>
    </b-list-group>
    <b-button @click="prev" variant="primary" href="#">prev</b-button>

    <b-button @click="clicked()" variant="primary" href="#">Submit</b-button>
    <b-button @click="next" variant="success" href="#">Next</b-button>
  </b-jumbotron>
</div>
</template>

<script>
import lodash from "lodash";
export default {
    props: {
        qurrentQuestion: Object,
        next: Function,
        prev: Function
    },
    data() {
      return {
        selected: null,
        correctIndex: 0,
        submit: false,
        correct: false,
        shuffleAnswers: []
      }
    },
    computed: {
        answers() {
            let answers = [...this.qurrentQuestion.incorrect_answers];
            answers.push(this.qurrentQuestion.correct_answer);
            return answers;
        }
    },
    watch: {
      qurrentQuestion() {
        this.selected  = null;
        this.shuffledAnswers();
      }
    },
    methods: {
      select(index) {

        this.selected = index
        

      },
      clicked() {
        this.submit = true;
      }
      ,
      submited(index) {
        let className = ''

        switch (index) {
          case this.correctIndex && this.submit:
            className = "correct"
            break;

          case this.selected:
            className = "selected"
          break;
        
          default:
            className = ''
            break;
        }
        return className;

        

      }
      ,
      shuffledAnswers() {
            let answers = [...this.qurrentQuestion.incorrect_answers]
            answers.push(this.qurrentQuestion.correct_answer);
            this.shuffleAnswers = lodash.shuffle(answers);
            this.correctIndex = this.shuffleAnswers.indexOf(this.qurrentQuestion.correct_answer)

      }
    }
}

</script>

<style  scoped>

.list-group-item:hover {
  background: #eeeeee;
  cursor: pointer;
}
.selected {
  background: rgb(94, 94, 224);
}
.selected:hover {
  background: rgb(94, 94, 224);
}
.correct {
  background: rgb(98, 241, 98);
}
.correct:hover {
  background: rgb(98, 241, 98);
}
.wrong {
  background: rgb(241, 72, 72);
}

.wrong:hover {
  background: rgb(241, 72, 72);
}

.btn {
  margin-top: 40px;
}
</style>