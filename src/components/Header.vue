<template>
  <div class="container">
    <nav>
      <img src="../assets/bee-1.png" alt="bee" :class="{ rotated: revealed }" />

      <h1>{{ text }}</h1>
      <button @click="reveal">
        <img
          src="../assets/bee-2.png"
          alt="bee"
          :class="{ rotated: revealed }"
        />
      </button>
    </nav>
    <div class="rind"></div>
  </div>
</template>

<script>
export default {
  props: {
    text: String,
  },
  data() {
    return {
      revealed: false,
    };
  },
  methods: {
    reveal() {
      this.revealed = !this.revealed;
      this.$emit("reveal", { state: this.revealed });
    },
  },
};
</script>

<style scoped>
.container {
  height: 5.75rem;
}

button {
  background: none;
  font-family: inherit;
  border: none;
  font-size: inherit;
  cursor: pointer;
  /* align-self: flex-start; */
  line-height: inherit;
  display: inline;
  position: relative;
  height: 1em;
}

nav {
  background: var(--yellow-gradient);
  display: grid;
  grid-template-columns: auto auto auto;
  align-items: center;
  padding: var(--spacing-half);
  font-size: 1.5rem;
  line-height: 1.3;
  justify-content: center;
  position: relative;
  color: #fff;
  overflow: hidden;
  height: calc(100% - 0.5rem);
}

@media (min-width: 768px) {
  nav {
    font-size: 1.75rem;
  }
}

@media (min-width: 1024px) {
  nav {
    font-size: 2.5rem;
  }
}

.rind {
  height: 0.5rem;
  width: 100%;
  background: #000;
}

h1 {
  font-size: 1em;
  /* white-space: nowrap; */
  hyphens: auto;
  text-align: center;
  color: black;
}

img {
  height: 1em;
  width: auto;
  margin: 0 0.5em;
  transform: rotate(0deg);
}

button > img {
  /* transform: rotate(180deg); */
}

button > img.rotated {
  transform: rotate(-25deg);
  /* filter: hue-rotate(300deg); */
}

img.rotated {
  transform: rotate(25deg);
  /* filter: hue-rotate(-140deg); */
}
</style>