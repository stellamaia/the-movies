<template>
  <div class="nav-bar-component">
    <nav class="navbar fixed-top container-nav">
      <button
        class="navbar-toggler"
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
        <div class="offcanvas-body">
          <ul class="navbar-nav justify-content-end flex-grow-1 pe-3">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#"
                >favoritos</a
              >
            </li>
          </ul>
        </div>
      </div>

      <router-link class="icon" to="/login">
        <i class="material-symbols-outlined icon person">person</i>
      </router-link>
    </nav>
  </div>
</template>

<script>
export default {
  name: "NavBar",
  props: {
    msg: String,
  },
};
</script>

<style lang="scss">
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
.offcanvas.offcanvas-start {
  width: 40%;
}
</style>
