<script>
import axios from 'axios';
export default {
  data() {
    return {
      enteredMovieName: '',
      movieInfo: [],
      isLoading: true,
      inputError: '',
    };
  },
  methods: {
    loadMovieDetail() {
      if (this.enteredMovieName.length === 0) {
        this.isLoading = true;
        this.inputError = 'Please enter a Movie or Series name';
      } else {
        this.movieInfo = [];
        axios
          .get(
            `http://www.omdbapi.com/?t=${this.enteredMovieName}&apikey=ec7b2d29`
          )
          .then((response) => {
            this.isLoading = false;
            const res = response.data;

            this.movieInfo.push({
              id: res.Title,
              title: res.Title,
              year: res.Year,
              plot: res.Plot,
              actors: res.Actors,
              genre: res.Genre,
              awards: res.Awards,
              img: res.Poster,
            });
            console.log(this.movieInfo);
          })
          .catch(function () {
            throw new Error('not working');
          });
      }
    },
  },
};
</script>

<template>
  <section class="m-24 text-cyan-600 text-center font-mono">
    <div class="mb-20">
      <h1 class="text-slate-50">Movie Detail</h1>
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
      {{ inputError }}
    </div>
    <div v-else>
      <li
        v-for="(detail, info) in movieInfo"
        :key="info.id"
        class="bg-fuchsia-800"
      >
        <h3>
          Title: <span> {{ detail.title }}</span>
        </h3>
        <h4>
          Year Of Movie: <span> {{ detail.year }}</span>
        </h4>
        <p>
          Plot: <span> {{ detail.plot }}</span>
        </p>
        <h4>
          Actors: <span>{{ detail.actors }}</span>
        </h4>
        <h4>
          Genre: <span>{{ detail.genre }}</span>
        </h4>
        <h4>
          Awards: <span> {{ detail.awards }}</span>
        </h4>
      </li>
    </div>
  </section>
</template>

<style>
* {
  background-color: black;
}
li {
  list-style-type: none;
}
</style>
