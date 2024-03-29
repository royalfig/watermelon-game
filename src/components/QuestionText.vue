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
      <button @click="$emit('question', { number: null })">
        <svg
          fill="currentColor"
          class="bi bi-arrow-left-circle-fill"
          viewBox="0 0 16 16"
        >
          <path
            d="M8 0a8 8 0 1 0 0 16A8 8 0 0 0 8 0zm3.5 7.5a.5.5 0 0 1 0 1H5.707l2.147 2.146a.5.5 0 0 1-.708.708l-3-3a.5.5 0 0 1 0-.708l3-3a.5.5 0 1 1 .708.708L5.707 7.5H11.5z"
          />
        </svg>
      </button>
    </article>
  </div>
</template>

<script>
import questionData from "../assets/questions.json";
export default {
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
  color: var(--dark-green);
  background: rgba(255, 255, 255, 0.95);
  padding: var(--spacing);
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
    padding: var(--spacing);
  }
}

.confetti {
  background-image: url("../assets/confetti.png");
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
  background: var(--green-gradient);
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

button {
  font-size: 2rem;
  padding: 5px;
  font-family: inherit;
  background: none;
  border: none;
  background: var(--green-gradient);
  color: rgba(255, 255, 255, 0.9);
  border-radius: 50%;
  box-shadow: var(--shadow);
  cursor: pointer;
  transition: background 0.2s, box-shadow 0.2s;
  margin: 0.5rem 0;
  line-height: 1;
  position: absolute;
  left: 0;
  top: 50%;
  height: 3rem;
  width: 3rem;
  transform: translate(-50%, -50%);
}

button:hover {
  background: var(--pink-gradient);
  box-shadow: var(--shadow-lg);
}

button svg {
  height: 100%;
  width: 100%;
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