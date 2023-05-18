<template>
  <div class="nav-bar-component">
    <nav class="navbar container-nav">
      <router-link to="/">
      <i class="material-symbols-outlined menu">menu</i>
    </router-link> 

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
.nav-bar-component{
  background-color: #000000;
}
.container-nav {
  display: flex;
  padding: 15px;
}
.menu{
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

  &person{
    font-size: 32px;
  }
}
</style>
