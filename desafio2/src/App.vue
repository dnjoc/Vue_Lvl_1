<script setup>
import { reactive, ref } from "vue";
const varBoton = ref("country-code");
const varFlex = ref("display: flex;");
const Cliente = reactive({
  Nombre: "CADI F1 C.A.",
  linkCanal: "@Cadif1AcademiaSoftware",
  nroSuscriptores: "5,16 K",
  nroVideos: "238",
  descripcionBreve:
    "CADI F1 C.A. Academia de Software. Entrenamos personas en el uso de herramientas tecnológicas, preparándolas para trabajar.",
  imgLogo: "public/cadif1_logo.jpg",
  imgBanner: "public/cadif1_cover.jpg",
  imgFacebook: "public/facebook.png",
  imgInstagram: "public/instagram.png",
});
function clickElemento(info) {
  console.log(info);
  alert(`Click en: ${info}`);
}
const urlLogo = reactive({
  url: "public/YouTube-Logo-Vector.png",
});
const noSuscrito = ref("Suscribirme");
const siSuscrito = ref("Suscrito");
const suscrito = ref(false);
const busqueda = ref("");
</script>
<template>
  <header>
    <nav id="nav" class="navbar navbar-expand-sm bg-body-light">
      <div id="primerDivNav" class="container divNav">
        <a class="navbar-brand" href="#">
          <i class="bi bi-list"></i>
        </a>
      </div>
      <div class="container divNav">
        <a style="margin: 0" class="navbar-brand" href="#">
          <img v-bind:src="urlLogo.url" width="auto" height="24" />
        </a>
        <span :class="varBoton">VE</span>
      </div>
      <div class="container" style="width: auto">
        <form class="container-fluid">
          <div style="width: 40vw" class="input-group">
            <input
              type="search"
              id="search"
              class="form-control"
              placeholder="Buscar"
              aria-label="Buscar"
              aria-describedby="basic-addon1"
            />
            <span class="iconS input-group-text" id="basic-addon1"
              ><i class="bi bi-search"></i
            ></span>
          </div>
        </form>
        <span class="input-group-text iconMic"
          ><i class="bi bi-mic-fill"></i
        ></span>
      </div>
      <div id="ultimoDivNav" class="container divNav">
        <a class="navbar-brand" href="#">
          <i class="bi bi-camera-video"></i>
        </a>
        <a class="navbar-brand" href="#">
          <i class="bi bi-bell"></i>
        </a>
        <a class="navbar-brand" href="#">
          <img
            class="iconMic"
            src="https://images.unsplash.com/flagged/photo-1570612861542-284f4c12e75f?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
            width="37"
            height="37"
          />
        </a>
      </div>
    </nav>
  </header>
  <main>
    <div :style="varFlex">
      <nav id="navMain" class="nav flex-column">
        <a
          class="navbar-brand"
          style="background-color: rgb(232, 232, 232)"
          href="#"
        >
          <i class="bi bi-house-door"></i>
          <p>Inicio</p>
        </a>
        <a class="navbar-brand" href="#">
          <i class="bi bi-caret-right-square"></i>
          <p>Shorts</p>
        </a>
        <a class="navbar-brand" href="#">
          <i class="bi bi-collection-play"></i>
          <p>Suscripciones</p>
        </a>
        <a class="navbar-brand" href="#">
          <i class="bi bi-cast"></i>
          <p>Mi biblioteca</p>
        </a>
      </nav>
      <div @click="clickElemento('Banner')" id="banner" class="container">
        <img v-bind:src="Cliente.imgBanner" alt="banner" />
        <div @click.stop="clickElemento('Enlace de Redes')" id="redes">
          <img
            class="redes"
            src="https://app.cadif1.com//img/iconos/logo.ico"
            alt="cadi"
          />
          <p class="m-0 ms-1 fw-bold">Web</p>
          <img
            class="redes"
            v-bind:src="Cliente.imgInstagram"
            alt="instagram"
          />
          <img class="redes" v-bind:src="Cliente.imgFacebook" alt="facebook" />
        </div>
      </div>
    </div>
    <div id="datos" class="container">
      <img v-bind:src="Cliente.imgLogo" alt="" />
      <div v-if="suscrito" class="container">
        <h4 style="text-transform: uppercase">{{ Cliente.Nombre }}</h4>
        <p style="text-transform: uppercase">
          {{ Cliente.linkCanal }} {{ Cliente.nroSuscriptores }} suscriptores
          {{ Cliente.nroVideos }} videos
        </p>
        <p style="text-transform: uppercase">{{ Cliente.descripcionBreve }}</p>
      </div>
      <div v-else class="container">
        <h4 style="font-style: italic">{{ Cliente.Nombre }}</h4>
        <p style="font-style: italic">
          {{ Cliente.linkCanal }} {{ Cliente.nroSuscriptores }} suscriptores
          {{ Cliente.nroVideos }} videos
        </p>
        <p style="font-style: italic">{{ Cliente.descripcionBreve }}</p>
      </div>
      <div id="botones" class="container">
        <button
          v-if="suscrito" @click="suscrito = false"
          style="color: black; background-color: rgb(232, 232, 232)"
          type="button"
          class="btn btn-outline-dark btn-sm"
        >
          <i class="bi bi-bell"></i> {{ siSuscrito }}
          <i class="bi bi-chevron-down"></i>
        </button>
        <button
          v-else @click="suscrito = true"
          type="button"
          class="btn btn-outline-light btn-sm bg-dark"
        >
          {{ noSuscrito }}
        </button>
      </div>
    </div>
    <section id="nav2" class="container">
      <nav class="navbar navbar-expand-lg">
        <div class="container-fluid">
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <i class="bi bi-chevron-left"></i>
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <a class="nav-link" href="#">Videos</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#">Shorts</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#">En Directo</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#">Listas</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#">Comunidad</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#">Canales</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#">Informacion</a>
              </li>
            </ul>
            <form id="formBuscar" class="d-flex" role="search">
              <span class="buscar"><i class="bi bi-search"></i></span>
              <input
                v-model="busqueda"
                id="buscar"
                class="form-control me-2"
                type="search"
                placeholder="Buscar"
                aria-label="Search"
              />
            </form>
            <i class="bi bi-chevron-right"></i>
          </div>
        </div>
      </nav>
    </section>
    <div class="container">
      <h1 class="contenidoSearch">{{ busqueda }}</h1>
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}
.country-code {
  font-size: small;
}
#banner {
  position: relative;
}
#redes {
  width: 30px;
  display: flex;
  position: relative;
  z-index: 100;
  top: -10%;
  float: right;
  right: 6%;
  align-items: center;
}
.redes {
  margin-left: 15px;
  width: 25px !important;
  height: 25px;
}
#nav2 {
  display: flex;
  justify-content: space-around;
}
.nav-item {
  margin: 0 15px;
  font-weight: bold;
}
#buscar {
  border: none;
  border-radius: 0;
  border-bottom: 1px solid rgb(101, 101, 101);
}
#formBuscar {
  align-items: center;
}
@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    /* padding-right: calc(var(--section-gap) / 2); */
  }
  main {
    display: flex;
    flex-direction: column;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
