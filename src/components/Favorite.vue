<template>
  <div>
    <span
      v-if="!isFavorite"
      class="btn-favorite"
      type="button"
      @click="addToFavorites(movie)"
    >
      <img src="../assets/favorite.svg" alt="icon favorite background" />
    </span>

    <span v-else>
      <svg
        id="heart-svg"
        height="40"
        width="40"
        viewBox="467 392 58 57"
        xmlns="http://www.w3.org/2000/svg"
        @click="removeFromFavorites(movie)"
      >
        <g id="Group" fill-rule="evenodd" transform="translate(467 392)">
          <path
            d="M29.144 20.773c-.063-.13-4.227-8.67-11.44-2.59C7.63 28.795 28.94 43.256 29.143 43.394c.204-.138 21.513-14.6 11.44-25.213-7.214-6.08-11.377 2.46-11.44 2.59z"
            id="heart"
            fill="red"
          />
        </g>
      </svg>
    </span>

    <button
      type="button"
      class="icon-close"
      data-bs-dismiss="modal"
      aria-label="Close"
    >
      <i class="material-symbols-outlined">close</i>
    </button>
  </div>
</template> 

<script>
export default {
  name: "FavoriteComponent",
  data() {
    return {
      isFavorite: false,
      favorites: [],
      movieList: [],
    };
  },
  props: {
    movie: Object,
  },
  created() {
    this.verifyFavorites();
  },
  methods: {
    showFavorites() {
      const favorites = JSON.parse(localStorage.getItem("favorites")) || [];
      this.favorites = favorites;
    },
    addToFavorites(movie) {
      const favorites = JSON.parse(localStorage.getItem("favorites")) || [];
      const existingMovie = favorites.find(
        (favMovie) => favMovie?.id === movie?.id
      );

      if (existingMovie) {
        return;
      }
    
      favorites.push(movie);
      localStorage.setItem("favorites", JSON.stringify(favorites));
      this.isFavorite = !this.isFavorite; 
    },
    removeFromFavorites(movie) {
      this.isFavorite = false;
      const favorites = JSON.parse(localStorage.getItem("favorites"));
      const updatedFavorites = favorites.filter((fav) => fav?.id !== movie?.id);
      localStorage.setItem("favorites", JSON.stringify(updatedFavorites));
    },
    verifyFavorites() {
      const favorites = JSON.parse(localStorage.getItem("favorites"));
      const existingMovie = favorites?.find(
        (favMovie) => favMovie?.id === this.movie?.id
      );
      if (existingMovie) {
        this.isFavorite = true;
      }
    },
  },
};
</script>
<style scoped lang="scss">
.icon-close {
  color: white;
  border: none;
  background-color: rgba(255, 0, 0, 0);
  top: 8px;
  right: 4px;
  position: absolute;
}
#heart-svg {
  cursor: pointer;
}
</style>