<template>
  <article>
    <div class="num">
      <img :src="require(`../assets/${num}.png`)" />
    </div>
    <p class="topic">{{ category }}</p>
    <button @click="$parent.$emit('question', { number: num })">⮩</button>
  </article>
</template>

<script>
export default {
  props: {
    num: Number,
    category: String,
    text: String,
    bonus: String,
    answer: String,
    bonusAnswer: String,
  },
};
</script>

<style scoped>
article {
  background: rgba(255, 255, 255, 0.95);
  color: #000;
  box-shadow: var(--shadow);
  border-radius: var(--radius);
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  overflow: hidden;
  margin-bottom: var(--spacing);
}

.num {
  padding: var(--spacing-half) var(--spacing);
  height: 250px;
  box-shadow: var(--shadow-lg);
  border-radius: var(--radius);
  margin: 0.55rem;
}

.num img {
  height: 100%;
}

.topic {
  font-size: 2.2rem;
  text-align: center;
  padding: var(--spacing);
}

button {
  font-size: 4rem;
  padding: var(--spacing-half) var(--spacing);
  font-family: inherit;
  background: none;
  border: none;
  background-color: var(--watermelon);
  color: #fff;
  border-radius: var(--radius);
  box-shadow: var(--shadow-lg);
  cursor: pointer;
  transition: background-color 0.2s, box-shadow 0.2s;
  margin: 0.5rem;
}

button:hover {
  background-color: var(--dark-green);
}

button:active {
  box-shadow: var(--shadow);
}
</style>