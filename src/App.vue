<script setup>
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div>
    <h1>{{ quizTitle }}</h1>
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
      <button @click="checkAnswer" :disabled="selectedOption === null">{{ nextButton }}</button>
    </div>
    <div v-else>
      <h2>{{ quizResult }}</h2>
      <button @click="restartQuiz">{{ restartButton }}</button>
    </div>
    <button @click="changeLanguage">{{ languageButton }}</button>
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
      quizTitle: "Generation Quiz",
      currentQuestion: 0,
      selectedOption: null,
      correctAnswers: 0,
      quizComplete: false,
      quizResult: null,
      nextButton: "Next",
      restartButton: "Restart Quiz",
      languageButton: "Change Language"
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
    },
    changeLanguage() {
      if (this.quizTitle === "Generation Quiz") {
        this.quizTitle = "Quiz da Geração";
        this.nextButton = "Próxima";
        this.restartButton = "Reiniciar Quiz";
        this.languageButton = "Mudar Idioma";
        this.quizData[0].question = "Qual plataforma vc usa mais ?";
        this.quizData[1].question = "Qual dessas series vc prefere mais ?";
        this.quizData[2].question = "Qual seu jeito favorito de escutar musica ?";
        this.quizData[3].question = "Qual seu jeito favorito de fazer compras";
        this.quizData[4].question = "Como vc se comunica com seus amigos?";


      } else {
        this.quizTitle = "Generation Quiz";
        this.nextButton = "Next";
        this.restartButton = "Restart Quiz";
        this.languageButton = "Change Language";
        this.quizData[0].question = "Which social media platform do you use the most ?";
        this.quizData[1].question = "Which of these TV shows do you enjoy the most ?";
        this.quizData[2].question = "What is your favorite way to listen to music ?";
        this.quizData[3].question = "What is your favorite way to shop ?";
        this.quizData[4].question = "What is your favorite way to communicate with friends ?";

      }
    }}
  }
  </script>