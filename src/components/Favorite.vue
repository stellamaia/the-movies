<template>
  <div>
    <span
      v-if="!isClicked"
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
      isClicked: false,
      favorites: [],
      movieList: []
    };
  },
  methods: {
   
    showFavorites() {
      //Obtém a lista de favoritos do LocalStorage
      const favorites = JSON.parse(localStorage.getItem("favorites")) || [];
      this.favorites = favorites;
      // console.log(this.favorites);
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
      this.isClicked = !this.isClicked;
      // Adicionar lógica aqui para adicionar ou remover dos favoritos
    },
    removeFromFavorites(movie) {
      this.isClicked = false;
      // Lógica para remover dos favoritos
      // Exemplo: Remover do localStorage
      const favorites = JSON.parse(localStorage.getItem("favorites"));
      const updatedFavorites = favorites.filter((fav) => fav.id !== movie.id);
      localStorage.setItem("favorites", JSON.stringify(updatedFavorites));
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
</style>