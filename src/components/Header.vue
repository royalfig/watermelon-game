<template>
  <div class="container">
    <nav>
      <img src="../assets/watermelon.png" alt="watermelon" />
      <h1>{{ text }}</h1>
      <img src="../assets/watermelon.png" alt="watermelon" />
    </nav>
    <div class="rind"></div>
  </div>
</template>

<script>
export default {
  props: {
    text: String,
  },
};
</script>

<style scoped>
.container {
  height: 4.775rem;
}

button {
  background: none;
  font-family: inherit;
  border: none;
  font-size: inherit;
  cursor: pointer;
  align-self: flex-start;
}
nav {
  background: var(--green-gradient);
  display: flex;
  align-items: center;
  padding: var(--spacing-half);
  font-size: 1.75rem;
  line-height: 1.3;
  justify-content: center;
  position: relative;
  color: #fff;
}

.rind {
  height: 0.5rem;
  width: 100%;
  background: #fff;
}

h1 {
  font-size: 1em;
}

img {
  height: 1em;
  margin: 0 0.5em;
}
img:last-of-type {
  transform: rotate(180deg);
}
</style>