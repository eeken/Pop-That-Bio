<template>
  <div class="container-fluid navbar navbar-fixed">
    <nav class="nav-extended">
      <div class="nav-wrapper">
        <router-link to="/">
          <a class="brand-logo">
            <p>POP THAT BIO</p>
          </a>
        </router-link>
        <a href="#" data-target="mobile-demo" class="sidenav-trigger">
          <i class="fas fa-align-justify"></i>
        </a>
        <ul class="right hide-on-med-and-down">
          <li class="nav-item">
            <router-link to="/movies" class="nav-link">FILMER</router-link>
          </li>

          <li class="nav-item">
            <router-link to="/about" class="nav-link">OM OSS</router-link>
          </li>
          <li class="nav-item">
            <div class="nav-link modal-trigger" data-target="modal-login">LOGGA IN</div>
          </li>
          
        </ul>
        
      </div>
    </nav>

    <!-- SIGN UP MODAL -->
    <div id="modal-signup" class="modal">
      <div class="modal-content">
        <h4 class="white-text text-grey lighten-5">Skapa konto</h4>
        <br />
        <form id="signup-form">

        <div class="row">
        <div class="input-field col s6">
          <input placeholder="" id="first_name" type="text" class="validate">
          <label for="first_name"><p class="white-text text-grey lighten-5">Förnamen</p></label>
        </div>
        <div class="input-field col s6">
          <input id="last_name" type="text" class="validate">
          <label for="last_name"><p class="white-text text-grey lighten-5">Efternamn</p></label>
        </div>
      </div>
          <div class="input-field">
            <input type="email" id="signup-email" required />
            <label for="signup-email"><p class="white-text text-grey lighten-5">Epost adress</p></label>
          </div>
          <div class="input-field">
            <input type="password" id="signup-password" required />
            <label for="signup-password "><p class="white-text text-grey lighten-5">Välj lösenord</p></label>
          </div>
         <div>
          <button class="btn yellow darken-2 z-depth-0">fortsättning</button> <button class="nav-link modal-trigger btn yellow darken-2 z-depth-0" data-target="modal-signup" >avboka</button>
         </div>
        </form>
      </div>
    </div>

    <!-- LOGIN MODAL -->
    <div id="modal-login" class="modal">
      <div class="modal-content">
        <h4 class="white-text text-grey lighten-5">Logga in</h4>
        <br />
        <form id="login-form">
          <div class="input-field">
            <input type="email" id="login-email" required />
            <label for="login-email"><p class="white-text text-grey lighten-5">Epost adress</p></label>
          </div>
          <div class="input-field">
            <input type="password" id="login-password" required />
            <label for="login-password "><p class="white-text text-grey lighten-5">Välj lösenord</p></label>
          </div>
          <div>
          <button class="btn yellow darken-2 z-depth-0">Logga in</button> <button class="nav-link modal-trigger btn yellow darken-2 z-depth-0" data-target="modal-signup" >Skapa konto</button>
        </div>
      
        </form>
      </div>
    </div>

    <ul class="sidenav" id="mobile-demo">
      <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />
      <router-link to="/mypage">
        <i class="large material-icons white-text text-grey lighten-5">account_circle</i>
      </router-link>
      <li class="nav-item">
        <router-link to="/">
          <a class="brand-logo">
            <p class="white-text text-grey lighten-5">HEM</p>
          </a>
        </router-link>
      </li>
      <li class="nav-item">
        <router-link to="/movies" class="nav-link">
          <p class="white-text text-grey lighten-5">FILMER</p>
        </router-link>
      </li>

      <li class="nav-item">
        <router-link to="/about" class="nav-link">
          <p class="white-text text-grey lighten-5">OM OSS</p>
        </router-link>
      </li>
      <li class="nav-item">
        <router-link to="/about" class="nav-link">
          <p class="white-text text-grey lighten-5">Medlemmar</p>
        </router-link>
      </li>
      <li class="nav-item">
        <router-link to="/about" class="nav-link">
          <p class="white-text text-grey lighten-5">Frågor och svar</p>
        </router-link>
      </li>
      <li class="nav-item">
        <router-link class="nav-link" to="/signin">
          <p class="white-text text-grey lighten-5">Kundservice</p>
        </router-link>
      </li>
      <li class="nav-item">
          <a>  <div class="nav-link modal-trigger" data-target="modal-login"> 
              <p class="white-text text-grey lighten-5">LOGGA IN</p></div></a>
          </li>
    </ul>
  </div>
</template>
<script>
import M from 'materialize-css'
import firebase from "firebase";

export default {
  data() {
    return {
      email: '',
      password: '',
      email1: '',
      password1: '',
      isLoggedIn: false
    }
  },
  mounted() {
    var elems = document.querySelectorAll(".carousel");
    this.$M.Carousel.init(elems);
    setTimeout(this.$M.Carousel.init(elems), 1000);

    var modals = document.querySelectorAll(".modal");
    M.Modal.init(modals);

    var items = document.querySelectorAll(".collapsible");
    M.Collapsible.init(items);
  },
  methods: {
      signUp(e) {
      firebase
        .auth()
        .createUserWithEmailAndPassword(this.email, this.password)
        .then(
          user => {
            window.console.log(`Account created for ${user.email}`)
            this.$router.push("/mypage");
            const modal = document.querySelector('#modal-signup')
            M.Modal.getInstance(modal).close()
            this.email = ''
            this.password = ''
          },
          err => {
            alert(err.message);
          }
        );

      e.preventDefault();
    },
    logIn(e){
      e.preventDefault();
      firebase
        .auth()
        .signInWithEmailAndPassword(this.email, this.password)
        this.$router.push("/mypage");
        window.console.log('u are logged in')
        this.isLoggedIn = true
        const modal = document.querySelector('#modal-login')
            M.Modal.getInstance(modal).close()
            this.email = ''
            this.password = ''
      
    },
    logOut(e){
      firebase
        .auth()
        .signOut()
        .then(() => {
            window.console.log('u logged out')
            this.$router.push("/");
            this.isLoggedIn = false
          },
          err => {
            alert(err.message);
          }
        );

      e.preventDefault();
    }
    
  }
};
</script>

<style lang="css" scoped>
@font-face {
  font-family: borntogrille;
  src: url("../assets/fonts/borntogrille.otf");
}
nav {
  padding: 0 14.8%;
  border-bottom: 1px solid rgb(213, 187, 47);
  background: rgb(100, 10, 60);
  background: -webkit-linear-gradient(
    to top,
    rgb(156, 36, 100),
    rgba(197, 49, 99, 0.5)
  );
  background: linear-gradient(
    to bottom,
    rgb(117, 9, 67),
    rgba(197, 49, 99, 0.5)
  );
  text-shadow: 2px 4px 1px rgb(12, 1, 1);
  font-family: borntogrille;
}

.sidenav,.modal {
  background-color: rgb(107, 22, 72);
}
.modal {
 background: linear-gradient(to top, rgb(117, 9, 67), rgb(219, 166, 195));}

.our-brand-logo {
  font-size: 2.5rem;
  padding-left: 1.5%;
  font-family: borntogrille;
  text-shadow: 1px 6px 1px rgb(12, 1, 1);
}

.our-brand-logo:hover {
  color: rgb(243, 144, 197);
}

@media (max-width: 460px) {
  .our-brand-logo {
    font-size: 5vw;
  }
}

#nav-mobile .nav-item .nav-link {
  font-size: 1.2em;
}
.nav-link:hover {
  color: rgb(243, 144, 197);
}

.router-link-active {
  background: rgb(150, 38, 97);
}

@media (min-width: 481px) and (max-width: 767px) {
  nav {
    padding: 0;
  }
  .brand-logo {
    font-size: 2rem;
  }
}

@media (min-width: 320px) and (max-width: 480px) {
  nav {
    padding: 0;
  }
  .brand-logo {
    font-size: 1.9rem;
  }
}
</style>