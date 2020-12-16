<template>
  <div class="questionBox-container">
    <b-jumbotron>
      <template #lead>
        {{ question.question }} 
       </template>

      <hr class="my-4">

      <b-list-group>
        <b-list-group-item 
        v-for="(answer, index) in answers" 
          :key="index" 
          @click="selectAnswer(index)"
          :class="[selectedIndex === index ? 'selected' : '']"
          >{{ answer }}
          </b-list-group-item>
      </b-list-group>

      <b-button variant="primary" href="#">SUBMIT</b-button>
      <b-button @click="next" variant="success" href="#">NEXT</b-button>
    </b-jumbotron>
    <hr class="my-4" />
  </div>
</template>

<script>
import _ from  'lodash'
export default {
  props: {
    question: Object,
    next: Function,
  },

  data() {
    return {
      selectedIndex: null,
      shuffledAnswers: []
    }
  },

  computed: {
    answers() {
      let answers = [...this.question.incorrect_answers];
       answers.push(this.question.correct_answer);
       return answers;
    }
  },
  
  watch: {
    question() {
      this.selectedIndex = null
      this.shuffleAnswers()
    }
  },

  methods: {
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    shuffleAnswers() {
      let answers = [...this.question.incorrect_answers, this.question.correct_answercorrect_answer]
      this.shuffledAnswers = _.shuffle(answers)
    }
  },

  mounted() {
    console.log(this.question);
  }
}
</script>

<style scoped>
.list-group{
  margin-bottom: 15px;
}

.list-group-item:hover {
  background-color: rgb(214, 245, 234);
  cursor: pointer;
}

.btn {
  margin: 0 5px;
}

.selected {
  background-color: mediumaquamarine;
}

.correct {
  background-color: green;
}

.incorrect {
  background-color: red;
}
</style>