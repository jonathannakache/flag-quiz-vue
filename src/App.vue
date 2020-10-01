<template>
  <div id="app">
    <h1>
      TEST : Saurez-vous reconnaître ces pays par leur drapeau ?
    </h1>
    <card v-for="(item, index) in flags" :key="index" :flag="item"></card>

    <div class="card">
      <img
        :src="`https://flagcdn.com/w640/${flags[index].flag}.png`"
        class="card-img-top"
        :alt="`Drapeau du ${flags[index].country} `"
      />
      <ul class="list-group">
        <li
          v-for="(item, index) in flags[index].answers"
          :key="index"
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
  methods: {},
  data() {
    return {
      flags: flags,
      index: 3,
    };
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
  width: 50%;
  margin: 0 auto;
}
.list-group-item {
  cursor: pointer;
  font-size: 18px;
}
.list-group-item:hover {
  background: rgb(148, 205, 230);
}
</style>
