<script setup>
import { reactive, ref } from 'vue';
const varBoton = ref('country-code');
const varFlex = ref('display: flex;');
const Cliente = reactive({
  Nombre: "CADI F1 C.A.",
  linkCanal: "@Cadif1AcademiaSoftware",
  nroSuscriptores: "5,16 K",
  nroVideos: "238",
  descripcionBreve: "CADI F1 C.A. Academia de Software. Entrenamos personas en el uso de herramientas tecnológicas, preparándolas para trabajar.",
  imgLogo: 'public/cadif1_logo.jpg',
  imgBanner: 'public/cadif1_cover.jpg',

});
const urlLogo = reactive({
  url: 'public/YouTube-Logo-Vector.png'
});
 const noSuscrito = ref('Suscribirme');
 const siSuscrito = ref('Suscrito');
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
    <a style="margin: 0;" class="navbar-brand" href="#">
      <img v-bind:src="urlLogo.url" width="auto" height="24">
    </a>
    <span :class="varBoton">VE</span>
  </div>
  <div class="container" style="width: auto;">
    <form class="container-fluid">
      <div style="width: 40vw;" class="input-group">
        <input  type="search" id="search" class="form-control" placeholder="Buscar" aria-label="Buscar" aria-describedby="basic-addon1">
        <span class="iconS input-group-text" id="basic-addon1"><i class="bi bi-search"></i></span>
      </div>
    </form>
    <span class="input-group-text iconMic"><i class="bi bi-mic-fill"></i></span>
  </div>
  <div id="ultimoDivNav" class="container divNav">
    <a class="navbar-brand" href="#">
      <i class="bi bi-camera-video"></i>
    </a>
    <a class="navbar-brand" href="#">
      <i class="bi bi-bell"></i>
    </a>
    <a class="navbar-brand" href="#">
      <img class="iconMic" src="https://images.unsplash.com/flagged/photo-1570612861542-284f4c12e75f?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D" width="37" height="37">
    </a>
  </div>
</nav>
  </header>
<main>
  <div :style="varFlex">

    <nav id="navMain" class="nav flex-column">
    <a class="navbar-brand" style="background-color: rgb(232, 232, 232);" href="#">
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
<div id="banner" class="container">
<img v-bind:src="Cliente.imgBanner" alt="">
</div>
  </div>
<div id="datos" class="container">
<img v-bind:src="Cliente.imgLogo" alt="">
<div class="container">
<h4>{{ Cliente.Nombre }}</h4>
<p>{{ Cliente.linkCanal }} {{ Cliente.nroSuscriptores }} suscriptores {{ Cliente.nroVideos }} videos</p>
<p>{{ Cliente.descripcionBreve }}</p>
</div>
<div id="botones" class="container">
  <button style="color: black; background-color: rgb(232, 232, 232);" type="button" class="btn btn-outline-dark btn-sm "><i class="bi bi-bell"></i> {{ siSuscrito }} <i class="bi bi-chevron-down"></i></button>
  <button type="button" class="btn btn-outline-light btn-sm bg-dark"> {{ noSuscrito }}</button>
</div>
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
