<template>
  <div id="app" class="container">
    <h1>
      TEST : Saurez-vous reconnaître ces pays par leur drapeau ?
    </h1>
    <div class="alert alert-info text-center">
      Votre score est : {{ score }} / {{ flags.length }}
    </div>
    <div class="card my-5">
      <img
        :src="`https://flagcdn.com/w640/${flags[index].flag}.png`"
        class="card-img-top"
        :alt="`Drapeau du ${flags[index].country} `"
      />
      <ul class="list-group">
        <li
          v-for="(item, index) in flags[index].answers"
          :key="index"
          @click="handleClick(index)"
          class="list-group-item"
        >
          {{ item }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import flags from "./flags";
export default {
  name: "App",
  components: {},
  data() {
    return {
      flags: flags,
      index: 0,
      score: 0,
    };
  },
  methods: {
    handleClick(index) {
      if (index === this.flags[this.index].ok) {
        this.score++;
        this.index++;
      } else {
        this.index++;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.card {
  width: 45%;
  margin: 0 auto;
}
.list-group-item {
  cursor: pointer;
  font-size: 18px;
}
.list-group-item:hover {
  background: rgb(184, 222, 238);
}
</style>
