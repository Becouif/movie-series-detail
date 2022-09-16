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
              yearOfReleased: res.Released,
            });
          })
          .catch(function () {
            throw new Error('not working');
          });
      }
    },
  },
};
</script>

<template class="bg-inherit">
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
  <section class="m-24 text-center bg-inherit">
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
    <div v-if="isLoading" class="max-w-sm rounded overflow-hidden shadow-lg">
      <span class="text-slate-50 text-base">{{ inputError }}</span>
    </div>
    <!-- start of the card for display content -->
    <div v-else>
      <div
        class="max-w-sm rounded overflow-hidden shadow-lg"
        v-for="detail in movieInfo"
        :key="detail.id"
      >
        <img class="w-full" :src="detail.img" :alt="detail.title" />
        <div class="px-6 py-4 my-detail-p">
          <div class="font-bold text-xl mb-2">{{ detail.title }}</div>
          <p class="text-base">Year:{{ detail.year }}</p>
          <p class="text-base">Plot: {{ detail.plot }}</p>
          <p class="text-base">Awards: {{ detail.awards }}</p>
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
li {
  list-style-type: none;
}
div.my-title {
  color: #831010;
  font-family: 'Ultra', serif;
  font-size: 30px;
}
h1.my-heading {
  /* font-family: 'Rakkas', cursive; */
  margin-top: 200px;
  margin-bottom: 20px;
}
div.my-detail-p {
  font-family: 'Mukta', sans-serif;
  color: white;
}
.my-btn:hover {
  margin-top: 20px;
  color: white;
  background-color: #831010;
  font-family: 'Mukta', sans-serif;
}
.my-btn {
  margin-top: 20px;
  background: none;
  color: white;
  border: 2px solid #831010;
}
.font-mukta {
  font-family: 'Mukta', sans-serif;
}

.bar {
  margin: 0 auto;
  width: 575px;
  border-radius: 30px;
  border: 1px solid #831010;
}
.bar:hover {
  box-shadow: 1px 1px 8px 1px #831010;
}
.bar:focus-within {
  box-shadow: 1px 1px 8px 1px #831010;
  outline: none;
}
.searchbar {
  height: 45px;
  border: none;
  width: 500px;
  font-size: 16px;
  outline: none;
  color: white;
}
</style>
