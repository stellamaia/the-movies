<template >
  <div class="login">
    <div class="nav-content">
      <router-link class="icon" to="/">
        <i class="material-symbols-outlined icon return">chevron_left</i>
      </router-link>
      <h2 class="login-title">The movies</h2>
    </div>
    <div class="content-login">
      <div class="container-login">
        <div>
          <h2 class="question-account">Você tem uma conta?</h2>
        </div>
        <form class="form">
          <div>
            <input
              type="email"
              class="form-control-email"
              id="exampleInputEmail1"
              aria-describedby="emailHelp"
              placeholder="Endereço de e-mail"
            />
          </div>
          <div>
            <input
              type="password"
              class="form-control-password"
              id="exampleInputPassword1"
              placeholder="senha"
            />
          </div>

          <div class="row">
            <div class="col-12 col-sm-12 col-md-6 col-lg-6 btn-login">
              <button class="btn-login enter">Enter</button>
            </div>
            <div class="col-12 col-sm-12 col-md-6 col-lg-6">
              <div class="forgot-password">
                <p
                  data-bs-target="#exampleModalToggle"
                  data-bs-toggle="modal"
                  class="forgot-password question"
                >
                  Forgot password?
                </p>
              </div>
            </div>
          </div>
        </form>
      </div>
    </div>

    <div
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
              Redefinir Senha
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
            Digite o e-mail que você usou no the movies,e enviaremos a você um
            link para redefinir a sua senha.
          </div>

          <form class="form">
            <div>
              <input
                type="email"
                class="form-control-email"
                id="exampleInputEmail2"
                aria-describedby="emailHelp"
                placeholder="Endereço de e-mail"
              />
            </div>
          </form>
          <div class="row modal-footer-btn">
            <div class="modal-footer col-12 col-sm-6 col-md-4 col-lg-4">
              <button
                class="btn-enter-modal"
                data-bs-target="#exampleModalToggle2"
                data-bs-toggle="modal"
              >
                Send
              </button>
            </div>
            <div class="modal-footer col-12 col-sm-6 col-md-4 col-mlg-4">
              <button
                type="button"
                class="btn-close-modal"
                data-bs-dismiss="modal"
                aria-label="Close"
              >
                Close
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div
      class="modal fade modal-enter"
      id="exampleModalToggle2"
      aria-hidden="true"
      aria-labelledby="exampleModalToggleLabel2"
      tabindex="-1"
    >
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="exampleModalToggleLabel2">
              E-mail enviado
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
            Procure o e-mail de redefinição de senha na caixa de entrada.
          </div>
          <div class="modal-footer">
            <button
              class="btn-close-modal white"
              data-bs-dismiss="modal"
              aria-label="Close"
            >
              Ok
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "LoginView",
  data() {
    return {
      email: "",
    };
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
    padding: 20px;
  }
}
.login-title {
  color: white;
  text-transform: uppercase;
  font-weight: 600;
  margin: 0px;
  display: flex;
  justify-content: center;
  padding: 50px;
}
.login {
  background-image: linear-gradient(to right bottom, #030328 60%, #5c0b5b 170%);
  height: 100vh;
}
.content-login {
  display: flex;
  justify-content: center;
}

.question-account {
  color: white;
  display: flex;
  justify-content: start;
  padding-top: 57px;
  padding-left: 20px;
  padding-bottom: 30px;
}

.form-control-email,
.form-control-password {
  background-color: rgba(187, 55, 55, 0);
  border: 1.5px solid rgba(193, 193, 193, 0.579);
  color: white;
  padding: 20px;
  margin-bottom: 30px;
  outline: none;
  border-radius: 5px;
  width: 100%;
}
.form-control-email:focus,
.form-control-password:focus {
  background-color: rgba(187, 55, 55, 0);
  border: 1.5px solid rgba(96, 50, 170, 0.579);
}
.form-control-email::placeholder,
.form-control-password::placeholder {
  color: white;
}

.content-btn {
  display: flex;
  justify-self: start;
}
.btn-login {
  margin-top: 30px;
  &.enter {
    border: none;
    color: white;
    border-radius: 5px;
    height: 50px;
    width: 130px;
    background-color: rgba(255, 255, 255, 0.05);
  }
}
.forgot-password {
  color: rgb(145, 129, 248);
  font-weight: 600;
  text-decoration: none;
  &.question {
    margin: 70px 0 0 0;
    cursor: pointer;
  }
}

.btn-enter-modal,
.btn-close-modal {
  height: 50px;
  width: 100%;
  font-weight: bold;
  
}

.container-login {
  background-color: rgba(221, 221, 221, 0.06);
  padding: 20px;
  border-radius: 10px;
}
.modal-footer {
 
    padding: 0;
  }
@media screen and (max-width: 480px) {
  .container-login {
    background-color: rgba(255, 0, 0, 0) !important;
  }
  .question-account {
    padding: 0 0 30px 0;
    margin: 0;
  }
  .btn-login {
    margin: 0;
  }

  .forgot-password {
    &.question {
      margin: 30px 0 0 0;
      cursor: pointer;
      font-size: 15px;
    }
  }

  .modal-footer {
    justify-content: center;
    padding: 0;
  }

}

@media screen and (min-width: 481px) and (max-width: 768px) {
 
  .container-login {
    background-color: rgba(255, 0, 0, 0) !important;
    padding: 20px;
    border-radius: 10px;
  }

  .btn-enter-modal,
  .btn-close-modal {
    height: 50px;
    width: 100%;
  }
  .btn-login {
    margin-top: 10px;
  }
  .forgot-password {
    &.question {
      margin: 34px 0 0 0;
      font-size: 15px;
    }
  }
}
@media screen and (min-width: 769px) and (max-width: 1024px) {

}
@media screen and (min-width: 1025px) and (max-width: 1200px) {
}
@media screen and (min-width: 1201px) {
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
.btn-enter-modal {
  border: none;
  color: white;
  border-radius: 5px;
  background-color: rgba(255, 255, 255, 0.05);
}
.btn-close-modal {
  color: white;
  border: none;
  border-radius: 5px;
  background-color: rgba(255, 255, 255, 0.05);
  &.white {
    color: rgb(16, 16, 15);
    background-color: white;
    font-weight: bold;
    text-transform: uppercase;
   
  }
}
</style>