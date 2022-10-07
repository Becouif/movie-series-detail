<script>
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
        this.isLoading = false;
        fetch(
          `https://www.omdbapi.com/?t=${this.enteredMovieName}&apikey=ec7b2d29`
        )
          .then((response) => {
            if (response.ok) {
              return response.json();
            }
          })
          .then((data) => {
            this.movieInfo.push({
              id: data.Title,
              title: data.Title,
              year: data.Year,
              plot: data.Plot,
              actors: data.Actors,
              genre: data.Genre,
              img: data.Poster,
              yearOfReleased: data.Released,
              type: data.Type,
              language: data.Language,
              country: data.Country,
              awards: data.Awards,
            });
          });
      }
    },
  },
};
</script>

<template>
  <!-- start of nav brand  -->
  <nav class="flex items-center justify-between flex-wrap p-6 bg-grey-50">
    <div class="flex items-center flex-shrink-0 mr-6 my-title">
      <svg
        class="fill-current h-8 w-8 mr-2"
        width="54"
        height="54"
        viewBox="0 0 54 54"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M13.5 22.1c1.8-7.2 6.3-10.8 13.5-10.8 10.8 0 12.15 8.1 17.55 9.45 3.6.9 6.75-.45 9.45-4.05-1.8 7.2-6.3 10.8-13.5 10.8-10.8 0-12.15-8.1-17.55-9.45-3.6-.9-6.75.45-9.45 4.05zM0 38.3c1.8-7.2 6.3-10.8 13.5-10.8 10.8 0 12.15 8.1 17.55 9.45 3.6.9 6.75-.45 9.45-4.05-1.8 7.2-6.3 10.8-13.5 10.8-10.8 0-12.15-8.1-17.55-9.45-3.6-.9-6.75.45-9.45 4.05z"
        />
      </svg>
      <span class="font-semibold tracking-tight">Movie Abstract</span>
    </div>
  </nav>
  <!-- end of nav brand with svg -->

  <!-- start of input and search button  -->
  <section class="m-24 text-center">
    <div class="">
      <div>
        <input
          @keyup.enter="loadMovieDetail"
          type="text"
          id="first_name"
          class="border text-sm rounded-lg block w-1/2 p-2.5 text-center"
          placeholder="search movie name"
          v-model="enteredMovieName"
          autofocus
        />
      </div>

      <button
        class="bg-transparent my-btn font-semibold hover:text-white py-2 px-4 border border-grey-700 hover:border-transparent rounded"
        @click="loadMovieDetail"
      >
        Submit
      </button>
    </div>
  </section>
  <section class="text-center font-mukta">
    <div
      v-if="isLoading"
      class="max-w-sm rounded overflow-hidden shadow-lg movie-card"
    >
      <span class="text-base">{{ inputError }}</span>
    </div>
    <!-- start of the card for display content -->
    <div v-else>
      <div
        class="max-w-sm rounded overflow-hidden shadow-lg movie-card"
        v-for="detail in movieInfo"
        :key="detail.id"
      >
        <img class="w-full" :src="detail.img" :alt="detail.title" />
        <div class="px-6 py-4 movie-card-p">
          <div class="text-base">
            <span class="font-bold">Title:</span> {{ detail.title }}
          </div>
          <p class="text-base">
            <span class="font-bold">Year:</span> {{ detail.year }}
          </p>
          <p class="text-base">
            <span class="font-bold">Plot:</span> {{ detail.plot }}
          </p>
          <p class="text-base">
            <span class="font-bold">Awards:</span> {{ detail.awards }}
          </p>
          <p class="text-base">
            <span class="font-bold">Actors:</span> {{ detail.actors }}
          </p>
          <p class="text-base">
            <span class="font-bold">Type:</span> {{ detail.type }}
          </p>
          <p class="text-base">
            <span class="font-bold">Language:</span> {{ detail.language }}
          </p>
          <p class="text-base">
            <span class="font-bold">Country:</span> {{ detail.country }}
          </p>
          <p class="text-base">
            <span class="font-bold">Year Of Release: </span>

            {{ detail.yearOfReleased }}
          </p>
        </div>
        <div class="px-6 pt-4 pb-2">
          <span
            class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2"
            >{{ detail.genre }}</span
          >
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
nav {
  background-color: #111827;
}
input {
  background-color: white;
  color: #111827;
  margin: auto;
}
li {
  list-style-type: none;
}
div.my-title {
  color: #e50914;
  font-family: 'Ultra', serif;
  font-size: 30px;
}
h1.my-heading {
  /* font-family: 'Rakkas', cursive; */
  margin-top: 200px;
  margin-bottom: 20px;
}
div.movie-card-p {
  font-family: 'Mukta', sans-serif;
  color: #111827;
}

div.movie-card {
  margin-left: auto;
  margin-right: auto;
  line-height: 3;
  margin-top: -4rem;
}
.my-btn {
  margin-top: 20px;
  color: white;
  background-color: #111827;
  font-family: 'Mukta', sans-serif;
}
.my-btn:hover {
  margin-top: 20px;
  background: none;
  color: #111827;
  border: 2px thin;
}
.font-mukta {
  font-family: 'Mukta', sans-serif;
}

/* start of media query for  input responsiveness  */
</style>
