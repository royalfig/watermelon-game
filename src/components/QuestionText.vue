<template>
  <div class="container">
    <article>
      <div class="category">
        <p>{{ question.category }}</p>
      </div>
      <p>{{ question.text }}</p>
      <transition name="slide-fade" mode="out-in">
        <div class="confetti" v-if="answers" key="confetti">
          <p class="answer">{{ question.answer }}</p>
        </div>
        <div class="media" key="question" v-else>
          <video controls v-if="question.type === 'video'">
            <source
              :src="require(`../assets/${question.media}`)"
              type="video/mp4"
            />
          </video>
          <img
            v-if="question.type === 'image'"
            :src="require(`../assets/${question.media}`)"
            alt="watermelon"
          />
        </div>
      </transition>
    </article>
    <answers :answers="question.answers" />
  </div>
</template>

<script>
import questionData from "../assets/questions.json";
import Answers from "../components/Answers.vue";

export default {
  components: {
    Answers,
  },

  props: {
    num: Number,
    answers: Boolean,
  },
  computed: {
    question() {
      const questions = questionData;
      return questions[this.$props.num - 1];
    },
  },
};
</script>

<style scoped>
.container {
  padding: var(--spacing-half);
  height: calc(100vh - 5.75rem);
  display: flex;
  align-items: center;
}

.answer {
  color: #fff;
  background: var(--blue);
  padding: var(--spacing);
  border: 5px solid #fff;
  box-shadow: var(--shadow-lg);
  border-radius: var(--radius);
}

article {
  width: 80vw;
  height: 100%;
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  color: #000;
  padding: var(--spacing-half);
  background: #fff;
  border-radius: var(--radius);
  font-size: 1rem;
  box-shadow: var(--shadow);
  position: relative;
}

@media (min-width: 768px) {
  article {
    font-size: 1.75rem;
    padding: var(--spacing-half) var(--spacing);
  }
}

.confetti {
  background-image: url("../assets/gold-confetti.png");
  background-repeat: none;
  border-radius: var(--radius);
  /* padding: 1rem; */
  height: calc(0.5625 * 90vmin);
  display: flex;
  align-items: center;
  justify-content: center;
  border: 4px dotted var(--watermelon);
}

.category {
  display: block;
  text-align: center;
  line-height: 1;
  font-size: 0.8rem;
}

p:not(.category) {
  margin: 1rem 0 2rem;
  text-align: center;
  font-size: 115%;
}

.category p {
  text-align: center;
  display: inline-block;
  font-size: 0.8rem;
  background: var(--yellow-gradient);
  padding: 0.5rem;
  border-radius: var(--radius);
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 2px;
}
.media {
  width: 90%;
  flex: 1;
  margin: 0 auto;
  position: relative;
  overflow: auto;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #000;
}

video,
img {
  height: 100%;
  width: 100%;
  position: absolute;
  left: 0;
  top: 0;
  padding: 0.25rem;
  border: 4px dotted var(--watermelon);
  margin: 0 auto;
  object-fit: contain;
}

.slide-fade-enter-active {
  transition: transform 0.4s ease-out, opacity 0.3s;
}

.slide-fade-leave-active {
  transition: transform 0.4s ease-in, opacity 0.3s;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  opacity: 0;
  transform: translateX(var(--spacing));
}
</style>