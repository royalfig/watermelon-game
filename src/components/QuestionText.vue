<template>
  <div class="container">
    <article>
      <p class="category">{{ question.category }}</p>
      <p>{{ question.text }}</p>
      <div class="media">
        <div class="responsive-shell">
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
      </div>
      <button @click="$emit('question', { number: null })">⮨</button>
    </article>
  </div>
</template>

<script>
import questionData from "../assets/questions.json";
export default {
  props: {
    num: Number,
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
  padding: var(--padding);
}

article {
  max-width: 932px;
  /* max-height: 932px; */
  margin: var(--spacing) auto;
  color: #000;
  padding: var(--spacing);
  background: #fff;
  border-radius: var(--radius);
  font-size: 2rem;
  box-shadow: var(--shadow);
  position: relative;
}

.category {
  position: absolute;
  top: 0;
  left: var(--padding);
  font-size: 0.8rem;
  background: var(--melon);
  padding: 0.2em;
  border-bottom-right-radius: 4px;
  border-bottom-left-radius: 4px;
}
p {
  margin-bottom: 2rem;
  hyphens: auto;
}

.responsive-shell {
  height: 0;
  width: 100%;
  padding-top: 56.25%;
  position: relative;
  border-radius: 4px;
  overflow: hidden;
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
}

img {
  object-fit: cover;
}

button {
  font-size: 2rem;
  padding: 0.25em;
  font-family: inherit;
  background: none;
  border: none;
  background: var(--green-gradient);
  color: #fff;
  border-radius: var(--radius);
  box-shadow: var(--shadow-lg);
  cursor: pointer;
  transition: background-color 0.2s, box-shadow 0.2s;
  margin: 0.5rem 0;
  line-height: 1;
  position: absolute;
  left: 0;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>