<template>
  <div
    class="container-app"
    :style="!movieList.length ? { height: '100vh' } : { height: '100%' }"
  >
    <div>
      <NavBar />

      <div
        id="carouselExampleInterval"
        class="carousel slide d-none d-lg-block"
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
            <div class="got"></div>
          </div>
          <div class="carousel-item" data-bs-interval="3000">
            <div class="tlou"></div>
          </div>
          <div class="carousel-item" data-bs-interval="3000">
            <div class="succession"></div>
          </div>
        </div>
      </div>

      <div
        id="carouselExampleInterval-2"
        class="carousel slide d-lg-none"
        data-bs-ride="carousel"
      >
        <div class="carousel-indicators">
          <button
            type="button"
            data-bs-target="#carouselExampleInterval-2"
            data-bs-slide-to="0"
            class="active button-one"
            aria-current="true"
            aria-label="Slide 1"
          ></button>
          <button
            type="button"
            data-bs-target="#carouselExampleInterval-2"
            data-bs-slide-to="1"
            class="button-two"
            aria-label="Slide 2"
          ></button>
          <button
            type="button"
            data-bs-target="#carouselExampleInterval-2"
            data-bs-slide-to="2"
            class="button-three"
            aria-label="Slide 3"
          ></button>
        </div>

        <div class="carousel-inner">
          <div class="carousel-item active" data-bs-interval="3000">
            <img
              src="../assets/got.webp"
              class="carousel-img-desktop carousel-img"
              alt="..."
            />
          </div>
          <div class="carousel-item" data-bs-interval="3000">
            <img
              src="../assets/tlou.jpg"
              class="carousel-img-desktop carousel-img"
              alt="..."
            />
          </div>
          <div class="carousel-item" data-bs-interval="3000">
            <img
              src="../assets/succession.jpeg"
              class="carousel-img-desktop carousel-img"
              alt="..."
            />
          </div>
        </div>
      </div>
      <div>
        <form
          style="padding-top: 30px"
          class="d-flex"
          @submit.prevent="getMovie"
          role="search"
        >
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

        <div class="row content-list-movie">
          <div
            class="col-6 movie mb-4"
            @click="verifyRatings(movie)"
            v-for="movie in movieList"
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
          </div>
        </div>
      </div>

      <div
        v-for="movie in movieList"
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
                class="modal-title"
                :id="'exampleModalToggleLabel-' + movie.id"
              >
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

            <div class="favorite"><Favorite :movie="movie" /></div>

            <div class="modal-body">
              <img
                class="img-modal"
                :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path"
                alt="Movie Poster"
              />
              <div class="content-details">
                <div class="content-assessment">
                  <span
                    :style="selectedStar >= star ? { color: 'orange' } : {}"
                    v-for="star in stars"
                    :key="star"
                    @click.stop="ratingMovie(star, movie)"
                    class="material-symbols-outlined content-assessment assessment"
                  >
                    star
                  </span>
                </div>
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
                  <p class="information films">
                    {{ movie.release_date }}
                  </p></span
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
    </div>
  </div>
</template>

<script>
import NavBar from "@/components/NavBar.vue";
import Favorite from "@/components/Favorite.vue";
import axios from "axios";

export default {
  name: "HomeView",
  data() {
    return {
      search: "",
      isClicked: false,
      movieList: [],
      stars: [1, 2, 3, 4, 5],
      selectedStar: 0,
      selectMovie: null,
    };
  },

  components: {
    NavBar,
    Favorite,
  },

  methods: {
    getMovie() {
      const apiKey = "c78faf8ccc0cf08a8c233cdb9fc3b51b";
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=${apiKey}&query=${this.search}`
        )
        .then((res) => {
          this.movieList = res.data.results;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    ratingMovie(star, movie) {
      // classifição do filme
      const ratings = JSON.parse(localStorage.getItem("ratings")) || [];
      const existingRating = ratings.find(
        (ratingMovie) => ratingMovie?.id === movie?.id
      );
      if (existingRating) {
        this.removeFromRatings(movie, star);
        return;
      }
      ratings.push({ ...movie, star });
      localStorage.setItem("ratings", JSON.stringify(ratings));
      this.selectedStar = star;
    },
    
    removeFromRatings(movie, star) {
      //Remove a classifição do filme
      this.selectedStar = star;
      const ratings = JSON.parse(localStorage.getItem("ratings"));
      const updatedRatings = ratings.map((rat) => {
        if (rat?.id === movie?.id) { 
        rat.star = star;
          return rat;
        }
      });
      localStorage.setItem("ratings", JSON.stringify(updatedRatings));
    },
    verifyRatings(movie) {
      //verifica as classifição
      const ratings = JSON.parse(localStorage.getItem("ratings"));
      const existingRatings = ratings?.find(
        (ratingMovie) => ratingMovie?.id === movie?.id
      );
      //Se existe, defini a star selecionada, como a star da classifição existente
      if (existingRatings) {
        this.selectedStar = existingRatings.star;
      } else {
      //senão, defini a star selecionada como 0
        this.selectedStar = 0;
      }
    },
  },
};
</script>
<style lang="scss" scoped>
.container-app {
  background-image: linear-gradient(to right bottom, #030328 60%, #5c0b5b 170%);
}
.favorite {
  display: flex;
  padding-right: 20px;
  justify-content: end;
}
.button-one,
.button-two,
.button-three {
  border-radius: 50%;
  height: 10px;
  width: 10px;
}
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

.modal-content {
  background-color: rgb(16 16 15);
}
.modal-title {
  color: white;
  text-align: center;
  font-size: 20px;
  padding: 0 15px 10px 15px;
}
.modal-header {
  border: none;
  padding: 40px 0 0 0;
  justify-content: center;
}
.modal-footer {
  border: none;
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

.carousel-img {
  width: 100%;
}
.content-list-movie {
  margin: 0;
  justify-content: center;
}
.movie {
  display: contents !important;
}

//heart
#heart-svg {
  transform-origin: center;
  animation: animateHeartOut-9ea40744 0.3s linear forwards;
}

@keyframes animateHeartOut-9ea40744 {
  0% {
    transform: scale(1.4);
  }
  100% {
    transform: scale(1);
  }
}
.content-assessment {
  cursor: pointer;
  justify-content: end;
  display: flex;
  &.assessment {
    color: #636363;
    margin: 5px;
  }
}
.carousel-item .got {
  background: url("../assets/got.webp") no-repeat center center scroll;
  width: 100%;
  min-height: 350px;
}

.carousel-item .tlou {
  width: 100%;
  min-height: 350px;
  background: url("../assets/tlou.jpg") no-repeat scroll;
}

.carousel-item .succession {
  width: 100%;
  min-height: 350px;
  background: url("../assets/succession.jpeg") no-repeat scroll;
}

@media screen and (max-width: 320px) {
  .search-input {
    padding: 20px 5px 20px 10px;
  }
  .search-input::placeholder {
    font-size: 14px;
  }
}

@media screen and (min-width: 321px) and (max-width: 480px) {
  .search-input {
    padding: 20px 5px 20px 10px;
  }
  .search-input::placeholder {
    font-size: 18px;
  }
}

.carousel-item .got {
  height: 70vh;
  min-height: 350px;
  background: url("../assets/got.webp") no-repeat center center scroll;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  object-fit: cover !important;
  background-position-y: 30%;
}

.carousel-item .tlou {
  height: 70vh;
  min-height: 350px;
  background: url("../assets/tlou.jpg") no-repeat scroll;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  object-fit: cover !important;
  background-position-y: 30%;
}

.carousel-item .succession {
  height: 70vh;
  min-height: 350px;
  background: url("../assets/succession.jpeg") no-repeat scroll;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  object-fit: cover !important;
  background-position-y: 40%;
}
@media screen and (min-width: 1025px) and (max-width: 1400px) {
  .card-poster {
    width: 238px;
    height: 276px;
  }
}

@media screen and (min-width: 1401px) {
  .card-poster {
    width: 250px;
    height: 330px;
  }
  .container-app {
    justify-content: center;
  }
  .carousel-img {
    width: 100%;
    height: 750px;
  }
}
</style>
