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
      <div class="card-body">
        <ul class="list-group">
          <li
            v-for="(item, index) in flags[index].answers"
            :key="index"
            @click="handleClick(index)"
            class="list-group-item  list-group-item-action"
            :class="{
              'list-group-item-success': verifReponse[index] == 'success',
              'list-group-item-danger': verifReponse[index] == 'danger',
            }"
          >
            {{ item }}
          </li>
        </ul>

        <button
          v-if="voirReponse"
          @click="continuer"
          class="btn btn-secondary mt-2"
        >
          Continuer
        </button>
      </div>
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
      voirReponse: false,
      verifReponse: [],
    };
  },
  methods: {
    handleClick(index) {
      this.voirReponse = true;
      if (index === this.flags[this.index].ok) {
        this.score++;
      } else {
        this.verifReponse[index] = "danger";
      }
      this.verifReponse[this.flags[this.index].ok] = "success";
    },
    continuer() {
      this.voirReponse = false;
      this.index++;
      this.verifReponse = [];
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

</style>
