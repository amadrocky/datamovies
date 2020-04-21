<template>
  <div>
    <b-navbar type="light" variant="dark">
      <b-nav-form @submit.prevent="search()">
        <b-form-input class="mr-sm-2" placeholder="Search" v-model="movieSearch"></b-form-input>
        <b-button variant="outline-danger" class="my-2 my-sm-0" type="submit"><i class="fas fa-search"></i> Search
        </b-button>
      </b-nav-form>
    </b-navbar>
    <b-container class="panel">
      <div id="info" v-if="infos !== null">
        <b-row v-if="infos.Title" class="pt-5">
          <b-col>
            <p><em class="text-danger">TITLE:</em> {{ infos.Title }}</p>
            <br/>
            <p><em class="text-danger">YEAR:</em> {{ infos.Year }}</p>
            <br/>
            <p><em class="text-danger">RUNTIME:</em> {{ infos.Runtime }}</p>
            <br/>
            <p><em class="text-danger">GENRE:</em> {{ infos.Genre }}</p>
            <br/>
            <p><em class="text-danger">DIRECTOR:</em> {{ infos.Director }}</p>
            <br/>
            <p><em class="text-danger">ACTORS:</em> {{ infos.Actors }}</p>
            <br/>
            <p><em class="text-danger">PLOT:</em> {{ infos.Plot }}</p>
            <br/>
            <p><em class="text-danger">COUNTRY:</em> {{ infos.Country }}</p>
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
        class="text-center py-3 m-0"
        show
      >Veuillez executer une recherche
      </b-alert>
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
<style scoped>
  .panel {
    background-color: black;
    padding: 20px;
    margin-top: 100px;
    color: white;
    border-radius: 10px;
    box-shadow: 0px 0px 5px black;
  }
</style>
