<template>
  <div class="answers__container">
    <button @click="$parent.$emit('question', { number: null })">
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
  /* padding: var(--spacing-half); */
  display: flex;
  flex-direction: column;
  background: transparent;
  justify-content: center;
  align-items: center;
  z-index: 10;
}

.answers__container div {
  flex: 1;
  text-align: center;
  font-size: 1.25rem;
  border-radius: var(--radius);
  border: 5px solid;
  padding: var(--spacing-half);
  margin: var(--spacing-half);
  background: #fff;
  box-shadow: var(--shadow);
}

span {
  text-transform: uppercase;
  font-weight: 900;
  color: var(--blue);
}

button {
  font-size: 2rem;
  padding: 5px;
  font-family: inherit;
  background: none;
  border: none;
  background: #000;
  color: rgba(255, 255, 255, 1);
  border-radius: 50%;
  box-shadow: var(--shadow);
  cursor: pointer;
  transition: background 0.2s, box-shadow 0.2s;
  margin: 0.5rem 0;
  line-height: 1;
  /* position: absolute;
  left: 0;
  top: 50%; */
  height: 3rem;
  width: 3rem;
  /* transform: translate(-50%, -50%); */
}

button:hover {
  background: var(--pink-gradient);
  box-shadow: var(--shadow-lg);
}

button svg {
  height: 100%;
  width: 100%;
}
</style>