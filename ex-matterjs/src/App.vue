<script>
import Simulation from "./components/Simulation.vue";

export default {
  components: {
    Simulation,
  },
};
</script>

<template>
  <section class="vue-home">
    <div class="container text-center text-light">
        <h1>Simulazione, attrito 0</h1>
      <div>
          <Simulation />
      </div>
    </div>
    
  </section>
</template>

<style lang="scss">
@use "./styles/general.scss";

.vue-home {
  color: #2c3e50;
  background: #181818;
  transition: color 0.5s, background-color 0.5s;
  line-height: 1.6;
  width: 100%;
  height: 100vh;
  font-family: Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue",
    sans-serif;
  font-size: 15px;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
