<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div>
    <h1>Generation Quiz</h1>
    <div v-if="!quizComplete">
      <h2>{{ currentQuestion + 1 }}. {{ quizData[currentQuestion].question }}</h2>
      <ul>
        <li v-for="(option, index) in quizData[currentQuestion].options" :key="index">
          <label>
            <input type="radio" :value="option" v-model="selectedOption">
            {{ option }}
          </label>
        </li>
      </ul>
      <button :disabled="selectedOption === null" @click="checkAnswer">Next</button>
    </div>
    <div v-else>
      <h2>{{ quizResult }}</h2>
      <button   @click="restartQuiz">Restart Quiz</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      quizData: [
        {
          question: "Which social media platform do you use the most?",
          options: ["Instagram", "Facebook", "Twitter"],
          answer: "Instagram"
        },
        {
          question: "Which of these TV shows do you enjoy the most?",
          options: ["Friends", "The Office", "Stranger Things"],
          answer: "Stranger Things"
        },
        {
          question: "What is your favorite way to listen to music?",
          options: ["CDs", "iTunes", "Spotify"],
          answer: "Spotify"
        },
        {
          question: "What is your favorite way to shop?",
          options: ["Online", "In-store", "Both"],
          answer: "Online"
        },
        {
          question: "What is your favorite way to communicate with friends?",
          options: ["Text", "Phone", "Social media"],
          answer: "Text"
        }
      ],
      currentQuestion: 0,
      selectedOption: null,
      correctAnswers: 0,
      quizComplete: false,
      quizResult: null
    };
  },
  methods: {
    checkAnswer() {
      if (this.selectedOption === this.quizData[this.currentQuestion].answer) {
        this.correctAnswers++;
      }

      if (this.currentQuestion < this.quizData.length - 1) {
        this.currentQuestion++;
        this.selectedOption = null;
      } else {
        this.quizComplete = true;

        if (this.correctAnswers >= 3) {
          this.quizResult = "You are from the Generation Z.";
        } else {
          this.quizResult = "You are from the Millennial generation.";
        }
      }
    },
    restartQuiz() {
      this.currentQuestion = 0;
      this.selectedOption = null;
      this.correctAnswers = 0;
      this.quizComplete = false;
      this.quizResult = null;
    }
  }
};
</script>




<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
