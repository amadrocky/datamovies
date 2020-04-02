<template>
  <div>
    <b-navbar type="light" variant="dark">
      <b-nav-form @submit.prevent="search()">
        <b-form-input class="mr-sm-2" placeholder="Search" v-model="movieSearch"></b-form-input>
        <b-button variant="outline-success" class="my-2 my-sm-0" type="submit">Search</b-button>
      </b-nav-form>
    </b-navbar>
    <b-container class="movieBlock p-3 my-3 mbs-3">
      <div id="info" v-if="infos !== null">
        <b-row v-if="infos.Title" class="pt-5">
          <b-col>
            <p>TITLE: {{ infos.Title }}</p>
            <br />
            <p>YEAR: {{ infos.Year }}</p>
            <br />
            <p>RUNTIME: {{ infos.Runtime }}</p>
            <br />
            <p>GENRE: {{ infos.Genre }}</p>
            <br />
            <p>DIRECTOR: {{ infos.Director }}</p>
            <br />
            <p>ACTORS: {{ infos.Actors }}</p>
            <br />
            <p>PLOT: {{ infos.Plot }}</p>
            <br />
            <p>COUNTRY: {{ infos.Country }}</p>
          </b-col>
          <b-col class="text-center">
            <b-img class="image" v-bind:src="infos.Poster" alt="cover"></b-img>
          </b-col>
        </b-row>
        <div v-else>
          <b-alert variant="warning" class="text-center mt-5" show>{{ infos.Error }}</b-alert>
        </div>
      </div>
      <b-alert
        v-else
        variant="primary"
        class="text-center mt-5"
        show
      >Veuillez executer une recherche</b-alert>
    </b-container>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";

Vue.use(VueAxios, axios);

export default {
  name: "Home",
  data: () => ({
    infos: null,
    movieSearch: ""
  }),
  methods: {
    search() {
      axios
        .get(`http://www.omdbapi.com/?t=${this.movieSearch}&apikey=8548d355`)
        .then(response => (this.infos = response.data))
        .catch(e => {
          console.log("error", e);
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .movieBlock {
    background-color: rgba(17, 16, 16, 0.6);
    border-radius: 5px;
    color: white;
  }
</style>
