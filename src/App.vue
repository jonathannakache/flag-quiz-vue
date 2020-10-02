<template>
  <div id="app" class="container">
    <h1 class="mt-2">
      TEST : Saurez-vous reconnaître ces pays par leur drapeau ?
    </h1>
    <div class="row d-flex justify-content-center">
      <div class="col-6">
        <div class="mt-2 alert alert-light text-center">
          Votre score est : {{ score }} / {{ flags.length }}
        </div>
      </div>
    </div>
    <div class="card my-2">
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
          v-if="voirReponse && !fin"
          @click="continuer"
          class="btn btn-secondary mt-2"
        >
          Continuer
        </button>
        <button v-if="fin" @click="recommencer" class="btn btn-secondary mt-2">
          recommencer
        </button>

        <div id="myModal" class="modal" tabindex="-1" role="dialog">
          <div class="modal-dialog" role="document">
            <div class="modal-content">
              <div class="modal-header">
                {{
                  score > flags.length / 2
                    ? "Bravo !!"
                    : "Peux  mieux faire ..."
                }}
                <h5 class="modal-title"></h5>
                <button
                  type="button"
                  class="close"
                  data-dismiss="modal"
                  aria-label="Close"
                >
                  <span aria-hidden="true">&times;</span>
                </button>
              </div>
              <div class="modal-body">
                <p>Votre score est : {{ score }} / {{ flags.length }}</p>
              </div>
              <div class="modal-footer">
                <button
                  type="button"
                  class="btn btn-secondary"
                  data-dismiss="modal"
                >
                  Fermer
                </button>
                <button
                  @click="recommencer"
                  type="button"
                  class="btn btn-primary"
                >
                  Recommencer
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import flags from "./flags";
import $ from "jquery";
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
      fin: false,
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
      if (this.index == this.flags.length - 1) {
        this.fin = true;
        $("#myModal").modal("show");
      }
    },
    continuer() {
      this.voirReponse = false;
      this.index++;
      this.verifReponse = [];
    },
    recommencer() {
      $("#myModal").modal("hide");
      this.fin = this.voirReponse = false;
      this.index = this.score = 0;
      this.verifReponse = [];
    },
  },
};
</script>

<style>
body {
  background: #ff7e5f; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #feb47b,
    #ff7e5f
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #feb47b,
    #ff7e5f
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: graƒyscale;
  text-align: center;
  color: #2c3e50;
}
.card {
  max-width: 500px;
  margin: 0 auto;
}
.card img {
  height: 250px;
}
.list-group-item {
  cursor: pointer;
  font-size: 18px;
}
</style>
