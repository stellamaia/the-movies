<template>
  <div class="home">
    <NavBar />

    <div
      id="carouselExampleInterval"
      class="carousel slide"
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
  </div>
</template>

<script>
// @ is an alias to /src
import NavBar from "@/components/NavBar.vue";

export default {
  name: "HomeView",
  data() {
    return {};
  },
  components: {
    NavBar,
  },
};
</script>
<style scoped>
.button-one,
.button-two,
.button-three {
  border-radius: 50%;
  height: 15px;
  width: 15px;
}
.carousel-item{
height: 100%;
}
</style>