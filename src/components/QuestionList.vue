<template>
  <div class="container">
    <button
      class="num"
      v-for="question in questions"
      :key="question.num"
      @click="$emit('question', { number: question.num })"
    >
      <img :src="require(`../assets/${question.num}.png`)" />
    </button>
  </div>
</template>

<script>
import questions from "../assets/questions.json";
export default {
  data() {
    return {
      questions,
    };
  },
};
</script>

<style scoped>
.container {
  height: calc(100vh - 5.75rem);
  margin: 0 auto;
  width: 80vw;
  display: grid;
  grid-template-columns: auto auto auto;
  justify-content: center;
  align-items: center;
  gap: var(--spacing);
}

.num {
  background: rgba(255, 255, 255, 0.95);
  padding: 1rem;
  height: 8rem;
  width: 8rem;
  object-fit: contain;
  box-shadow: var(--shadow);
  border-radius: var(--radius);

  border: none;
  cursor: pointer;
  transition: box-shadow 0.2s;
}

@media (min-width: 768px) {
  .num {
    height: 10rem;
    width: 10rem;
  }
}

.num:hover {
  box-shadow: var(--shadow-lg);
}

.num img {
  height: 100%;
  filter: saturate(95%) contrast(95%);
  transition: filter 0.2s;
}

.num:hover img {
  filter: saturate(125%) contrast(125%);
}
</style>