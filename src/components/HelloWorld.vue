<template>
  <mdb-container>
    <div class="navbar">
      <div class="logo-container">
        <img src="./assets/logo.png" class="media-object">
      </div>

      <div class="button-area">
        <!-- <button class="login-button" @click="login=true">Zaloguj</button> -->
        <mdb-btn color="cyan lighten-1" size="md" @click="login=true" class="waves-light">Zaloguj</mdb-btn>
      </div>

      <div class="top-menu">
        <!-- <a href="#" style="display: inline">Konta osobiste |</a>
        <a href="#" style="display: inline">Kredyty |</a>
        <a href="#" style="display: inline">Karty płatnicze |</a>
        <a href="#" style="display: inline">Oszczędności i inwestycje</a> -->

        <p style="display: inline; color: #2c3e50; font-size: 18px;">Kredyty |</p>
        <p style="display: inline; color: #2c3e50; font-size: 18px;">Konta osobiste |</p>
        <p style="display: inline; color: #2c3e50; font-size: 18px;">Karty płatnicze |</p>
        <p style="display: inline; color: #2c3e50; font-size: 18px;">Oszczędności</p>
      </div>
    </div>

    <div class="posts">
      <!-- <mdb-btn rounded color="default" @click="login=true">launch modal</mdb-btn> -->
      <!-- simple login modal -->

        <mdb-carousel :interval="2000" showControls class="car">
    <mdb-carousel-item img src="https://i.ibb.co/jwF9v03/desk-3139127-1920.jpg" alt="First slide" />
    <mdb-carousel-item img src="https://i.ibb.co/yfKH0BY/calculator-385506-1920.jpg" alt="Second slide" />
    <mdb-carousel-item img src="https://i.ibb.co/V9PkNp3/stock-1863880-1920.jpg" alt="Third slide" />
  </mdb-carousel>



      <mdb-modal v-if="login" @close="login = false">
        <mdb-modal-header class="text-center">
          <mdb-modal-title tag="h4" bold class="w-100">Zaloguj</mdb-modal-title>
        </mdb-modal-header>
        <p class="error" v-if="error">Błędny PIN lub hasło</p>
        <mdb-modal-body class="mx-3 grey-text">
          <mdb-input label="PIN" v-model="pin" icon="fas fa-terminal" type="email" class="mb-5" required/>
          <mdb-input label="Hasło" v-model="password" icon="lock" type="password"/>
        </mdb-modal-body>
        <mdb-modal-footer center>
          <!-- <mdb-btn @click="login = false">Login</mdb-btn> -->
          <mdb-btn color="blue" size="md" v-on:click="send" class="waves-light">Zaloguj</mdb-btn>
        </mdb-modal-footer>
      </mdb-modal>

      <mdb-row>
        <mdb-col lg="5">
          <mdb-view class="rounded z-depth-2 mb-lg-0 mb-4" hover>
            <img class="img-fluid" src="./assets/img4.png" alt="Sample image">
            <a>
              <mdb-mask overlay="white-slight" waves/>
            </a>
          </mdb-view>
        </mdb-col>
        <mdb-col lg="7">
          <h3 class="font-weight-bold mb-3 p-0">
            <strong>Doceniaj bliskość z dodatkową gotówką</strong>
          </h3>
          <p>
            Dodatkowa gotówka pozwoli ci kupić rzeczy o których od zawsze marzyłeś Ty i twoja rodzina.
          </p>

          <mdb-btn color="success" size="md" class="waves-light">Sprawdź</mdb-btn>
        </mdb-col>
      </mdb-row>
      <hr class="my-5">
      <mdb-row>
        <mdb-col lg="7">
          <h3 class="font-weight-bold mb-3 p-0">
            <strong>Znana marka</strong>
          </h3>
          <p>
            Nasi zadłużeni na łączną kwotę 3 mld USD klienci z ponad 300 krajów są tego najlepszym przykładem.
          </p>

          <mdb-btn color="pink" size="md" class="mb-lg-0 mb-4 waves-light">Sprawdź</mdb-btn>
        </mdb-col>
        
        <mdb-col lg="5">
          <mdb-view class="rounded z-depth-2 mb-lg-0 mb-4" hover>
            <img
              class="img-fluid"
              src="./assets/img3.png"
              alt="Sample image"
            >
            <a>
              <mdb-mask overlay="white-slight" waves/>
            </a>
          </mdb-view>
        </mdb-col>
      </mdb-row>
      <hr class="my-5">
      <mdb-row>
        <mdb-col lg="5">
          <mdb-view class="rounded z-depth-2 mb-lg-0 mb-4" hover>
            <img
              class="img-fluid"
               src="https://mdbootstrap.com/img/Photos/Others/img%20(34).jpg"
              alt="Sample image"
            >
            <a>
              <mdb-mask overlay="white-slight" waves/>
            </a>
          </mdb-view>
        </mdb-col>
        <mdb-col lg="7">


          <h3 class="font-weight-bold mb-3 p-0">
             <strong>Wymarzone wakacje!</strong>
          </h3>
          <p>
            Od zawsze marzyłeś aby wybrac się na wakacje na łonie natury? Dziś kredyt oprocentowany na 95% w BankApp pozwoli 
            ci je zrealizować!
          </p>

          <mdb-btn color="indigo" size="md" class="waves-light">Sprawdź</mdb-btn>
        </mdb-col>
      </mdb-row>
    </div>
  </mdb-container>
</template>

<script>
import {
  mdbContainer,
  mdbRow,
  mdbCol,
  mdbCard,
  mdbCardBody,
  mdbMask,
  mdbIcon,
  mdbView,
  mdbBtn,
  mdbNavbar,
  mdbNavbarBrand,
  mdbModal,
  mdbModalHeader,
  mdbModalBody,
  mdbModalFooter,
  mdbInput,
  mdbCarousel, mdbCarouselItem 
} from "mdbvue";

import router from '../router'
import axios from 'axios';

    export const HTTP = axios.create({
        baseURL: `http://localhost:8090/registration`,
        headers: {
            'Access-Control-Allow-Origin': '*'
        }
    });

export default {
  name: "HelloWorld",
  components: {
    mdbContainer,
    mdbRow,
    mdbCol,
    mdbCard,
    mdbCardBody,
    mdbMask,
    mdbIcon,
    mdbView,
    mdbBtn,
    mdbNavbar,
    mdbNavbarBrand,
    mdbModal,
    mdbModalHeader,
    mdbModalBody,
    mdbModalFooter,
    mdbInput,
    mdbCarousel, mdbCarouselItem 
  },
  data() {
    return {
      login: false,
      pin: null,
      password: null,
      error: false
    };
  },
  methods: {
    send: function() {
      console.log("true");
      HTTP.post(`http://localhost:8090/login`, {
        pin: this.pin,
        password: this.password
      }).then(response => {
        localStorage.Authorization = response.data;
        router.push('/dashboard');
      }, error => {
        this.error = true;
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 @import url('https://fonts.googleapis.com/css?family=Noto+Sans');

h3 {
  font-weight: normal;
  padding-top: 20px;
  padding-bottom: 30px;
}
p {
  color: #969696;
  margin-bottom: 0;
  font-size: 14px;
}
.container {
  width: 60%;
}

::placeholder {
  color: white;
  opacity: 1; /* Firefox */
}

.navbar {
  background-color: white;
  width: 60%;
  height: 90px;
  margin: auto;
  position: fixed;
  top: 0px;
  left: 20%;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 3px 1px -2px rgba(0, 0, 0, 0.2),
    0 1px 5px 0 rgba(0, 0, 0, 0.12);
  z-index: 50;
}

.button-area[data-v-656039f0] {
  /* height: 100%; */
  width: 140px;
  /* border: 0px solid aqua; */
  /* float: right; */
}

.login-button {
  background-color: #4caf50;
  border: none;
  color: white;
  /* padding: 15px 32px; */
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 22px 0px 0px 35px;
  cursor: pointer;
  background-color: #15a4cf;
  /* border-radius: 3px; */
  width: 110px;
  height: 40px;
}

.top-menu {
  height: 30%;
  width: 500px;
  border-top: 1px solid #c7c7c7;
  margin: auto;
  position: absolute;
  left: 240px;

  text-align: center;
  color: #29313e;
  padding-top: 10px;
  top: 27px;
}

.logo-container {
  float: left;
  height: 100%;
}

.media-object {
  width: 55%;
}

a {
  text-decoration: none;
  color: #29313e;
  transition: all 0.3s;
}

a:hover {
  color: #15a4cf;
}

.button {
  background-color: #4caf50;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 44px 0px 0px 0px;
  cursor: pointer;
  border-radius: 3px;
  width: 140px;
}

.button2 {
  background-color: #008cba;
}

/* h1 {
    color: #15a4cf;
    font-size: 32px;
} */

p {
  /* color: #232323; */
  font-size: 20px;
  padding-top: 10px;
}

.posts {
  margin-top: 150px;
  border: 0px solid aquamarine;
  box-shadow: 0 2px 2px 0 rgba(0, 0, 0, 0.14), 0 3px 1px -2px rgba(0, 0, 0, 0.2),
    0 1px 5px 0 rgba(0, 0, 0, 0.12);
  background-color: white;
}

.font-weight-bold {
  margin-top: 20px;
  font-family: 'Raleway', sans-serif;
}

.error {
  text-align: center;
  font-size: 16px;
  color: rgb(250, 67, 67);
  font-family: 'Noto Sans', sans-serif;
}

.car {
  height: 400px;
  margin-bottom: 50px;
}


</style>
