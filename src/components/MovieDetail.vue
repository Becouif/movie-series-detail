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
            });
            console.log(data.Title);
          });
      }
    },
  },
};
</script>

<template>
  <!-- start of nav brand  -->
  <nav class="flex items-center justify-between flex-wrap p-6">
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
      <span class="font-semibold tracking-tight">Movie Overview</span>
    </div>
  </nav>
  <!-- end of nav brand with svg -->

  <!-- start of input and search button  -->
  <section class="m-24 text-center">
    <div class="mb-20">
      <div class="bar">
        <input
          @keyup.enter="loadMovieDetail"
          class="searchbar font-mukta"
          type="text"
          name=""
          placeholder="search movie name"
          v-model="enteredMovieName"
        />
      </div>

      <button class="w-24 ml-2 my-btn" @click="loadMovieDetail">Submit</button>
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
          <div class="font-bold text-xl mb-2">{{ detail.title }}</div>
          <p class="text-base">Year:{{ detail.year }}</p>
          <p class="text-base">Plot: {{ detail.plot }}</p>
          <p class="text-base">Awards: {{ detail.awards }}</p>
          <p class="text-base">Actors: {{ detail.actors }}</p>
          <p class="text-base">
            Year Of Release:
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
  background-color: #0d0d0d;
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
  color: #0d0d0d;
}

div.movie-card {
  margin-left: auto;
  margin-right: auto;
  line-height: 3;
}
.my-btn:hover {
  margin-top: 20px;
  color: white;
  background-color: #0d0d0d;
  font-family: 'Mukta', sans-serif;
}
.my-btn {
  margin-top: 20px;
  background: none;
  color: #0d0d0d;
  border: 2px thin;
}
.font-mukta {
  font-family: 'Mukta', sans-serif;
}

.bar {
  margin: 0 auto;
  width: 40%;
  border-radius: 30px;
  border: 1px solid #0d0d0d;
}
.bar:hover {
  box-shadow: 1px 1px 8px 1px #0d0d0d;
}
.bar:focus-within {
  box-shadow: 1px 1px 8px 1px #0d0d0d;
  outline: none;
}
.searchbar {
  width: 100%;
  height: 45px;
  border: none;
  width: 40%;
  font-size: 16px;
  outline: none;
  color: #831010;
}

/* start of media query for  input responsiveness  */
</style>
