<template>
  <div id="app">
    <Header :text="text" @reveal="showAnswers" />
    <div class="container">
      <transition name="slide-fade" mode="out-in">
        <QuestionList v-if="!num" @question="logQuestion" key="question" />
        <QuestionText
          v-else
          :num="num"
          @question="logQuestion"
          :answers="answers"
          key="answer"
        />
      </transition>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuestionList from "./components/QuestionList.vue";
import QuestionText from "./components/QuestionText.vue";
export default {
  components: {
    Header,
    QuestionList,
    QuestionText,
  },
  data() {
    return {
      num: null,
      answers: false,
    };
  },
  computed: {
    text() {
      if (this.num) {
        return `Question ${this.num}`;
      } else {
        return "Lil' Watermelon Trivia";
      }
    },
  },
  methods: {
    logQuestion(e) {
      const { number } = e;
      this.num = number;
    },
    showAnswers(e) {
      const state = e.state;
      this.answers = state;
    },
  },
};
</script>

<style>
:root {
  --watermelon: #fa2a60;
  --melon: #f6b2bb;
  --light-green: #bedba6;
  --dark-green: #2a8a6e;

  --spacing-half: 1rem;
  --spacing: 2rem;
  --spacing-2x: 4rem;

  --radius: 2rem;

  --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  --shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
  --shadow-lg: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);

  --green-gradient: linear-gradient(
    to top,
    #bedba6,
    #9cc795,
    #79b286,
    #559e79,
    #2a8a6e
  );
  --pink-gradient: linear-gradient(
    to bottom,
    #f6b2bb,
    #fa97a5,
    #fc7a8e,
    #fc5977,
    #fa2a60
  );
}
*,
*::before,
*::after {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

html {
  font-size: 1rem;
  font-size: clamp(
    1rem,
    0.9038461538461539rem + 0.4807692307692308vw,
    1.625rem
  );
  color: #fff;
}

#app {
  background: url("./assets/seeds-rotated.png"), var(--pink-gradient);
  background-size: 1000px 1000px, 100% 100%;
  background-position: 0 150%, 0 0;
  background-repeat: repeat-x, no-repeat;
  min-height: 100vh;
  height: 100%;
  font-family: "Fredoka One", sans-serif;
  font-weight: 400;
  background-blend-mode: darken;
  overflow: hidden;
}
.slide-fade-enter-active {
  transition: opacity 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: opacity 0.3s ease-in;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  opacity: 0;
}
</style>
