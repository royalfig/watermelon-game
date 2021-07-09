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
  max-width: 932px;
  margin: var(--spacing-2x) auto;
}

.num {
  background: rgba(255, 255, 255, 0.95);
  padding: 1rem;
  height: 250px;
  width: 250px;
  object-fit: contain;
  box-shadow: var(--shadow);
  border-radius: var(--radius);
  margin: 0.55rem;
  border: none;
  cursor: pointer;
}

.num img {
  height: 100%;
}
</style>