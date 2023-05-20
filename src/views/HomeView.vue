<template>
  <div class="home">
    <NavBar />

    <div
      id="carouselExampleInterval"
      class="carousel slide carousel-img-desktop"
      data-bs-ride="carousel"
    >
      <div class="carousel-indicators">
        <button
          type="button"
          data-bs-target="#carouselExampleInterval"
          data-bs-slide-to="0"
          class="active button-one"
          aria-current="true"
          aria-label="Slide 1"
        ></button>
        <button
          type="button"
          data-bs-target="#carouselExampleInterval"
          data-bs-slide-to="1"
          class="button-two"
          aria-label="Slide 2"
        ></button>
        <button
          type="button"
          data-bs-target="#carouselExampleInterval"
          data-bs-slide-to="2"
          class="button-three"
          aria-label="Slide 3"
        ></button>
      </div>

      <div class="carousel-inner">
        <div class="carousel-item active" data-bs-interval="3000">
          <img src="../assets/got.webp" class="d-block w-100" alt="..." />
        </div>
        <div class="carousel-item" data-bs-interval="3000">
          <img src="../assets/tlou.jpg" class="d-block w-100" alt="..." />
        </div>
        <div class="carousel-item" data-bs-interval="3000">
          <img
            src="../assets/succession.jpeg"
            class="d-block w-100"
            alt="..."
          />
        </div>
      </div>
    </div>

    <form class="d-flex mt-3" @submit.prevent="getMovie" role="search">
      <input
        id="input-1"
        v-model="search"
        class="search-input me-2"
        type="search"
        placeholder="What are you looking for?"
        aria-label="Search"
        required
      />
      <button class="btn-search" type="submit">Search</button>
    </form>
   

    <div style="margin: 0">
      <div
        class="movie mb-4"
        v-for="movie in movie.results"
        :key="movie.id"
        data-target="#exampleModalLong"
      >
       <img
          data-bs-target="#exampleModalToggle"
          data-bs-toggle="modal"
          class="card-poster"
          :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path"
          alt="Movie Poster"
        />
      </div>
    </div>

    <div
      v-for="movie in movie.results"
      :key="movie.id"
      class="modal fade"
      id="exampleModalToggle"
      aria-hidden="true"
      aria-labelledby="exampleModalToggleLabel"
      tabindex="-1"
    >
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="exampleModalToggleLabel">
              {{ movie.title }}
            </h1>
            <button
              type="button"
              class="icon-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            >
              <i class="material-symbols-outlined">close</i>
            </button>
          </div>
          <div class="modal-body">
            <img
              class="img-modal"
              :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path"
              alt="Movie Poster"
            />
            <span> Language: <p>{{ movie.original_language }}</p></span>
            <span>Data de lançamento: <p>{{ movie.release_date }}</p></span>
            <span>Vote average: <p>{{ movie.vote_average }}</p></span>
            <span>Vote count: <p>{{ movie.vote_count }}</p></span>
            <span>Overview: <p>{{ movie.overview }}</p></span>
          </div>
        </div>
      </div>
    </div>

    <!-- {{ movie.results }} -->
  </div>
</template>

<script>
// @ is an alias to /src
import NavBar from "@/components/NavBar.vue";
import axios from "axios";

export default {
  name: "HomeView",
  data() {
    return {
      search: "",
      movie: [],
    };
  },
  components: {
    NavBar,
  },

  methods: {
    getMovie() {
      const apiKey = "c78faf8ccc0cf08a8c233cdb9fc3b51b";
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=${apiKey}&query=${this.search}`
        )

        .then((res) => {
          this.movie = res.data;
          this.search = "";
          if (this.movie.poster_path === null) {
            this.movie.poster_path = "";
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
<style lang="scss" scoped>
.home {
  /* background-image: linear-gradient(to bottom, #030328, #010108); */
  background-image: linear-gradient(to right bottom, #030328 60%, #5c0b5b 170%);
  /* height: 100vh; */
}
.button-one,
.button-two,
.button-three {
  border-radius: 50%;
  height: 15px;
  width: 15px;
}
.carousel-item {
  height: 100%;
}
// @media screen and (max-width: 768px) {
//   .carousel-img-desktop {
//     /* display: none; */
//   }
// }

.search-input {
  outline: none;
  border-radius: 6px;
  width: 100%;
  border: none;
  color: white;
  padding: 20px;
  margin: 20px;
  margin-bottom: 30px;
  background-color: rgba(255, 255, 255, 0.05);
}
.search-input::placeholder {
  color: rgb(204, 204, 204);
  font-weight: 400;
  font-size: 20px;
}
.btn-search {
  border: none;
  color: white;
  border-radius: 5px;
  height: 60px;
  width: 130px;
  margin: 20px;
  background-color: rgba(255, 255, 255, 0.05);
}

.card-poster {
  width: 160px;
  height: 225px;
  margin: 10px;
  cursor: pointer;
}

.movie {
  display: contents;
}
.modal-content {
  background-color: rgb(16 16 15);
  padding: 25px;
}
.modal-title {
  color: white;
}
.modal-header {
  border: none;
  padding: 0 0 20px 0;
}
.modal-footer {
  border: none;
  // justify-content: center;
}
.modal-body {
  color: white;
  text-align: start;
  padding: 0 0 20px 0;
}
.icon-close {
  color: white;
  border: none;
  background-color: rgba(255, 0, 0, 0);
}
.img-modal {
  width: 100%;
}
</style>