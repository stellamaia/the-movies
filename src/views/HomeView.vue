<template>
  <div>
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
    <div
      :style="search ? {} : { height: '100vh' }"
      class="stellinha"
    >
      <form class="d-flex" @submit.prevent="getMovie" role="search">
        <input
          id="input-1"
          v-model="search"
          class="search-input"
          type="search"
          placeholder="What are you looking for?"
          aria-label="Search"
        />
        <button class="btn-search" type="submit">
          <i class="material-symbols-outlined">Search</i>
        </button>
      </form>

      <div style="margin: 0" class="stellinha">
        <div
          class="movie mb-4"
          v-for="movie in movie.results"
          :key="movie.id"
          :data-bs-target="'#exampleModalToggle-' + movie.id"
        >
          <img
            v-if="movie.poster_path"
            :data-bs-target="'#exampleModalToggle-' + movie.id"
            data-bs-toggle="modal"
            class="card-poster"
            :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path"
            alt="Movie Poster"
          />
          <button @click="addToFavorites(movie)" class="btn-favorite">
            Add to Favorites
          </button>
        </div>
      </div>
    </div>
    <div
      v-for="movie in movie.results"
      :key="movie.id"
      class="modal fade"
      :id="'exampleModalToggle-' + movie.id"
      aria-hidden="true"
      :aria-labelledby="'exampleModalToggleLabel-' + movie.id"
      tabindex="-1"
    >
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h1
              class="modal-title fs-5"
              :id="'exampleModalToggleLabel-' + movie.id"
            >
              {{ movie.title }}
            </h1>
            <i style="background-color: red" class="material-symbols-outlined">favorite</i>

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
            <div class="content-details">
              <span v-if="movie.adult" class="information"
                >Content:
                <p class="information films">Adult</p></span
              >
              <span v-else class="information"
                >Content:
                <p class="information films">Not Adult</p></span
              >

              <span class="information"
                >Language:
                <p class="information films">
                  {{ movie.original_language }}
                </p></span
              >
              <span class="information"
                >Release date:
                <p class="information films">{{ movie.release_date }}</p></span
              >
              <span class="information">
                Vote average:
                <p class="information films">{{ movie.vote_average }}</p>
              </span>
              <span class="information"
                >Vote count:
                <p class="information films">{{ movie.vote_count }}</p></span
              >
              <span class="information">Overview:</span>
              <p class="information overview">{{ movie.overview }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- {{ movie.results }}  -->
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
      movie: {
        adult: true,
        posterPath: false,
      },
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
        })
        .catch((error) => {
          console.log(error);
        });
    },
    addToFavorites(movie) {
      //criar variavel
      // Obtém a lista de favoritos do LocalStorage ou inicializa como um array vazio
      let favorites = JSON.parse(localStorage.getItem("favorites")) || [];
      // verifica se o filme já está na lista de favoritos
      const existingMovie = favorites.find(
        (favMovie) => favMovie.id === movie.id
      );
      //se existe, retorna
      if (existingMovie) {
        return;
      }

      // Adiciona o filme à lista de favoritos
      favorites.push(movie);

      localStorage.setItem("favorites", JSON.stringify(favorites));
    },
  },
};
</script>
<style lang="scss" scoped>
.home,
.stellinha {
  background-image: linear-gradient(to right bottom, #030328 60%, #5c0b5b 170%);
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
  border-radius: 6px 0 0 6px;
  width: 100%;
  border: none;
  color: white;
  padding: 20px;
  margin: 20px 0 0 20px;
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
  height: 64px;
  border-radius: 0 6px 6px 0;
  width: 130px;
  margin: 20px 20px 0 0;
  background-color: rgba(255, 255, 255, 0.101);
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
}
.modal-title {
  color: white;
  text-align: center;
}
.modal-header {
  border: none;
  padding: 40px 0 0 0;
  justify-content: center;
}
.modal-footer {
  border: none;
  // justify-content: center;
}
.modal-body {
  color: white;
  text-align: start;
  padding: 25px;
}
.icon-close {
  color: white;
  border: none;
  background-color: rgba(255, 0, 0, 0);
  top: 8px;
  right: 4px;
  position: absolute;
}
.img-modal {
  width: 100%;
}
.content-details {
  padding-top: 40px;
}
.information {
  display: flex;
  font-weight: 600;
  &.films {
    padding-left: 6px;
    font-weight: 300;
  }
  &.overview {
    padding-top: 10px;
    font-weight: 300;
  }
}

@media screen and (max-width: 480px) {
  .search-input::placeholder {
    font-size: 17px;
  }
}

@media screen and (min-width: 481px) and (max-width: 768px) {
  .search-input::placeholder {
  }
}
// .icon-favorite{
//   color: rgb(119, 0, 255);
// //   padding-left: 10px;
// //   cursor: pointer;
// }

.icon-favorite {
  background: linear-gradient(to right, #2d50cf, #732be7);
}
.icon-favorite:hover {
  background: linear-gradient(to right, #2d50cf, #732be7);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;

  padding-left: 10px;
  cursor: pointer;
}
</style>