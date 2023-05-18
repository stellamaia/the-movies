<template >
  <div class="login">
    <!-- <NavBar /> -->

    <div>
      <router-link class="icon" to="/login">
        <i class="material-symbols-outlined icon return">chevron_left</i>
      </router-link>
    </div>
    <div class="container-login">
      <div>
        <h2 class="question-account">Você tem uma conta?</h2>
      </div>
      <form class="form">
        <div class="mb-3">
          <input
            type="email"
            class="form-control"
            id="exampleInputEmail1"
            aria-describedby="emailHelp"
            placeholder="Endereço de e-mail"
          />
        </div>
        <div class="mb-3">
          <input
            type="password"
            class="form-control"
            id="exampleInputPassword1"
            placeholder="senha"
          />
        </div>

        <div class="row">
          <div class="col md-6 lg-4">
            <button type="submit" class="btn-login">Enter</button>
          </div>
          <div class="col md-6 lg-4">
            <router-link class="forgot-password" to="/">
              <p class="forgot-password question">Forgot password?</p>
            </router-link>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
// import NavBar from "@/components/NavBar.vue";
export default {
  name: "LoginView",
  data() {},
  components: {
    // NavBar,
  },
};
</script>

<style scoped lang="scss">
.icon {
  color: white;
  font-size: 50px;
  display: flex;
  justify-content: start;
  text-decoration: none;
  background-color: rgba(255, 255, 255, 0);

  &.return {
    font-size: 50px;
    padding: 10px;
  }
}
.login {
  background-color: #000000;
  height: 100vh;
}
.container-login {
  border-radius: 10px;
}
.question-account {
  color: white;
  display: flex;
  justify-content: start;
  padding-top: 57px;
  padding-left: 20px;
}
.form {
  padding: 35px;
}
.form-control {
  background-color: rgba(187, 55, 55, 0);
  border: 1.5px solid rgba(193, 193, 193, 0.579);
  color: white;
}
.form-control::placeholder {
  color: white;
}
.form-control:focus {
  background-color: rgba(187, 55, 55, 0);
}
.content-btn {
  display: flex;
  justify-self: start;
}
.btn-login {
  border: none;
  color: white;
  border-radius: 5px;
  height: 50px;
  width: 130px;
  background-color: rgba(255, 255, 255, 0.05);
}
.forgot-password {
  color: rgb(145, 129, 248);
  font-weight: 600;
  text-decoration: none;

  &.question {
    margin: 10px 0 0 0;
  }
}

@media screen and (min-width: 520px) {
  .container-login {
    background-color: rgba(221, 221, 221, 0.06);
    margin: 60px;
    padding: 20px;
    border-radius: 10px;
  }
}

 @media screen and (min-width: 768px) {
   .container-login {
     background-color: rgba(221, 221, 221, 0.06);
     margin: 100px;
     padding: 20px;
     border-radius: 10px;
   }
 }
@media screen and (min-width: 1024px) {
  .container-login {
    margin: 100px 200px 200px 200px;
  }
}

@media screen and (min-width: 1280px) {
  .container-login {
    margin: 100px 300px 300px 300px;
  }
}

@media screen and (min-width: 1800px) {
  .container-login {
    margin: 100px 400px 400px 400px;
  }
}
</style>