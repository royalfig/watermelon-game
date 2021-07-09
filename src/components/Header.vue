<template>
  <nav>
    <img src="../assets/watermelon.png" alt="watermelon" />
    <h1>{{ text }}</h1>
    <img src="../assets/watermelon.png" alt="watermelon" />
  </nav>
</template>

<script>
export default {
  props: {
    text: String,
  },
};
</script>

<style scoped>
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
  justify-content: center;
  position: relative;
  color: #fff;
}

nav::after {
  height: 0.5em;
  width: 100%;
  position: absolute;
  content: "";
  background: #fff;
  bottom: 0;
  left: 0;
  transform: translateY(100%);
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