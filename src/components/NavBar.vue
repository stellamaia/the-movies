<template>
  <div class="nav-bar-component">
    <nav class="navbar fixed-top container-nav">
      <button
        @click="showFavorites()"
        class="navbar-toggler-menu"
        type="button"
        data-bs-toggle="offcanvas"
        data-bs-target="#offcanvasNavbar"
        aria-controls="offcanvasNavbar"
        aria-label="Toggle navigation"
      >
        <i class="material-symbols-outlined menu"> Menu </i>
      </button>

      <div
        class="offcanvas offcanvas-start"
        tabindex="-1"
        id="offcanvasNavbar"
        aria-labelledby="offcanvasNavbarLabel"
      >
        <div class="offcanvas-header">
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="offcanvas"
            aria-label="Close"
          ></button>
        </div>
        <div v-if="favorites.length > 0" class="offcanvas-body">
          <p class="title-favorite">Favorites</p>

          <ul class="navbar-nav justify-content-end flex-grow-1">
            <li
              class="nav-item"
              v-for="favorite in favorites"
              :key="favorite.id"
            >
              <p class="favorite-movies-title">{{ favorite.title }}</p>
              <Favorite />
              <img
                class="card-poster-favorite"
                :src="'https://image.tmdb.org/t/p/w500/' + favorite.poster_path"
                alt="Movie Poster Favorite"
              />
            </li>
          </ul>
        </div>
        <div v-else>
          <p class="title-favorite">No Favorites</p>
        </div>
      </div>

      <router-link class="icon" to="/login">
        <i class="material-symbols-outlined icon person">person</i>
      </router-link>
    </nav>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "NavBar",

  data() {
    return {
      favorites: [],
      movieList: [],
    };
  },
  props: {
    msg: String,
  },
  methods: {
    showFavorites() {
      //Obtém a lista de favoritos do LocalStorage
      const favorites = JSON.parse(localStorage.getItem("favorites")) || [];
      this.favorites = favorites;
      // console.log(this.favorites);
    },
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
  },
};
</script>

<style lang="scss" scoped>
.nav-bar-component {
  background-color: #030328;
}
.container-nav {
  padding: 15px;
}
.menu {
  color: white;
  font-size: 32px;
}

.icon {
  background-color: #3d3d4e;
  color: white;
  cursor: pointer;
  border-radius: 50%;
  height: 40px;
  width: 40px;

  &.person {
    font-size: 29px;
    padding-top: 3px;
  }
}

.title-favorite {
  font-weight: 600;
  font-size: 20px;
}
.favorite-movies-title {
  padding-bottom: 10px;
  margin: 0;
}
.card-poster-favorite {
  width: 60%;
}
.offcanvas.offcanvas-start {
  width: 20%;
}
@media screen and (max-width: 480px) {
  .offcanvas.offcanvas-start {
    width: 60%;
  }
  .card-poster-favorite {
    width: 100%;
  }
}
.navbar-toggler-menu {
  border: none;
  background-color: transparent;
}

@media screen and (min-width: 481px) and (max-width: 768px) {
  .offcanvas.offcanvas-start {
    width: 40%;
  }
  .card-poster-favorite {
    width: 100%;
  }
}
@media screen and (min-width: 769px) and (max-width: 1024px) {
  .offcanvas.offcanvas-start {
    width: 30%;
  }
  .card-poster-favorite {
    width: 100%;
  }
}
@media screen and (min-width: 1025px) and (max-width: 1200px) {
}
@media screen and (min-width: 1201px) {
}
</style>
