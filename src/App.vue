<script>
import axios from 'axios';
export default {
  data() {
    return {
      enteredMovieName: '',
      movieInfo: [],
      isLoading: false,
    };
  },
  methods: {
    loadMovieDetail() {
      axios
        .get('http://www.omdbapi.com/?t=game+of+thrones&apikey=ec7b2d29')
        .then((response) => {
          this.isLoading = true;
          const res = response.data;

          this.movieInfo.push({
            id: res.Title,
            title: res.Title,
            year: res.Year,
            plot: res.Plot,
            actors: res.Actors,
            genre: res.Genre,
            awards: res.Awards,
          });
          console.log(this.movieInfo);
        })
        .catch(function () {
          throw new Error('not working');
        });
    },
  },
};
</script>

<template>
  <section class="m-24 text-cyan-600 text-center">
    <div class="mb-20">
      <h1 class="text-slate-50 font-mono">Movie Detail</h1>
    </div>
    <div class="mb-20">
      <input
        class="hover:bg-white font-mono"
        type="text"
        name=""
        placeholder="search movie name"
        v-model="enteredMovieName"
      />
      <button
        class="bg-cyan-600 text-slate-50 hover:bg-cyan-400 w-24 ml-2 hover:text-black font-mono"
        @click="loadMovieDetail"
      >
        Submit
      </button>
    </div>
    <div v-if="isLoading">
      <li v-for="(detail, info) in movieInfo" :key="info.id">
        <h3>
          Title: <span> {{ detail.title }}</span>
        </h3>
        <h4>
          Year Of Movie: <span> {{ detail.year }}</span>
        </h4>
        <p>
          Plot: <span> {{ detail.plot }}</span>
        </p>

        <span>Actors: {{ detail.actors }}</span>
        <span>Genre: {{ detail.genre }}</span>
        <span>Awards: {{ detail.awards }}</span>
      </li>
    </div>
  </section>
</template>

<style>
* {
  background-color: black;
}
</style>
