<template>
  <div id="app">
    <img id="bee" src="./assets/bee-2.png" alt="" />
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
        return "BaBee Trivia";
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

  mounted() {
    let top1 = 60,
      right1 = 5,
      count = 1;

    const bee = document.getElementById("bee");

    bee.addEventListener("animationend", updateAnimation);
    updateAnimation();
    function updateAnimation() {
      function getRandomNum(bound1, bound2) {
        let min = bound1;
        let max = bound2;

        if (!bound2) {
          min =
            Math.max(0, bound1 - bound1) === 0
              ? getRandomNum(0, 100)
              : Math.max(0, bound1 - bound1);
          max =
            Math.min(100, bound1 * 5) === 100
              ? getRandomNum(0, 100)
              : Math.min(100, bound1 * 5);
        }
        return Math.floor(Math.random() * (max - min) + min);
      }

      function scaler(first, second) {
        if (first - second >= 0) {
          return "scaleX(1)";
        }
        return "scaleX(-1)";
      }

      let previous = [right1, top1];

      top1 = getRandomNum(previous[1]);

      right1 = getRandomNum(previous[0]);

      const template = `
      #bee {
        animation: beeFlight${count} 2s ease-out;
      }

      @keyframes beeFlight${count}  {

        from {
          right:${previous[0]}%;
          top: ${previous[1]}%;
          transform: ${scaler(right1, previous[0])} rotate(${getRandomNum(
        -25,
        25
      )}deg);

        }

        to {
          transform: ${scaler(right1, previous[0])} rotate(${getRandomNum(
        -25,
        25
      )}deg);
          right:${right1}%; 
          top: ${top1}%;
        }
     
    }`;
      const head = document.head;
      const animation = document.getElementById("animation");
      if (animation) {
        animation.remove();
      }
      const style = document.createElement("style");
      style.id = "animation";
      style.append(document.createTextNode(template));
      head.append(style);
      count++;
    }
  },
};
</script>

<style>
:root {
  --watermelon: #fae52a;
  --melon: #f3e567;
  --light-green: #111003;
  --dark-green: #3a370c;

  --spacing-half: 1rem;
  --spacing: 2rem;
  --spacing-2x: 4rem;

  --radius: 2rem;

  --shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
  --shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
  --shadow-lg: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);

  --yellow-gradient: linear-gradient(to top, #fae52a, #fcf191);
  --pink-gradient: linear-gradient(
    to bottom,
    #fae52a,
    #ffa146,
    #ff608f,
    #eb5ad7,
    #3774fa
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
  color: #000;
}

body {
  overflow: hidden;
}

#app {
  font-family: "Otomanopee One", sans-serif;
  font-weight: 400;
  background-blend-mode: darken;
  overflow: hidden;
}

.container {
  background: var(--pink-gradient);
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

#bee {
  position: absolute;
  width: 50px;
  height: auto;
  top: 60%;
  right: 5%;
  z-index: 1000;
  filter: drop-shadow(0 2px 0.5em rgba(0, 0, 0, 0.45));
}
</style>
