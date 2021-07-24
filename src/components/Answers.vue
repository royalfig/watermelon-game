<template>
  <div class="answers__container">
    <div v-for="(answer, i) in answers" :key="i">
      <p>
        <span>{{ letters[i] }}.</span> {{ answer }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    answers: Array,
  },

  data() {
    return {
      letters: ["a", "b", "c", "d"],
    };
  },
};
</script>

<style scoped>
.answers__container {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  /* padding: var(--spacing-half); */
  display: flex;
  background: transparent;
  justify-content: center;
  z-index: 10;
}

.answers__container div {
  flex: 1;
  text-align: center;
  font-size: 1.25rem;
  border-radius: var(--radius);
  border: 3px solid;
  padding: var(--spacing-half);
  margin: var(--spacing-half);
  background: var(--yellow-gradient);
}

span {
  text-transform: uppercase;
  font-weight: 900;
}
</style>