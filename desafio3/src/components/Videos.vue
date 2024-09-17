<script setup>
import { computed, ref, onMounted } from "vue";
import videosData from "../dataBase/videos.json";


let vds = ref([]);
vds = videosData.videos;
// console.log(videos.videos);
console.log(vds);
console.log("en componente videos");
console.log(vds.title)
const videoSeleccionado = ref(null);
function seleccionarVideo(idVideo) {
    console.log(`video seleccionado ${idVideo}`);
  videoSeleccionado.value = idVideo;
  console.log(videoSeleccionado.value);
  //modificar el style del video segun id con vue
};

   //cambiar background-color al div del videoSeleccionado
   
   function changeColor(id) {
    console.log("en funcion");
    console.log(id);
    console.log(this.elements);
      const element = document.getElementById(id);
      console.log("luego de la constante");
      console.log(element);
      element.style.backgroundColor = "green"; // Change to desired color
      console.log(isSelectionActive.value);
    };
    

const isSelectionActive = computed(() => {
  if (videoSeleccionado.value === null) {
    return "seleccion inactiva";
  } else {
    return "seleccion activa";
  }
});
onMounted(() => {
    console.warn('Evento onMounted disparado en Videos.vue');
    console.log(isSelectionActive.value);
})
</script>
<template >
    <section class="px-5 mx-5">
        <div class="encabezado">
            <h4>Cadi Fridays - Clases en Vivo</h4>
            <i class="bi bi-caret-right"></i>
            <h5>Reproducir todo</h5>
        </div>
        <div>
            <h5 class="m-4">{{ isSelectionActive }}</h5>
        </div>
        <div class="wrapper">
            <!-- <i id="left1" class="bi bi-chevron-left"></i> -->
            <div class="carousel">
                <div :class="{ selected: isSelectionActive }" class="row flex-row gap-1 justify-content-center" >
                    <div v-for="(videos, idx) in vds" :key="idx" :id="idx" @click="seleccionarVideo(idx), changeColor(idx)" class="card col-sm-3 mb-3 mb-sm-0" style="border: none; width: 13rem;">
                  <img :src="videos.urlImg" class="card-img" style="width: auto; height: 7rem;" alt="...">
                  <h5 class="tiempo">{{ videos.duration }}</h5>
                  <div class="card-body px-0">
                    <h5 class="card-title">{{ videos.title }}</h5>
                    <p class="card-text">CADI F1 C.A.</p>
                    <p class="card-text">{{ videos.views }} visualizaciones</p>
                    <p class="card-text">· Emitido hace {{ idx + 1 }} semanas</p>
                  </div> 
                </div>
                </div>
            </div>
            <!-- <i id="right1" class="bi bi-chevron-right"></i> -->
        </div>
        <hr>
       
    </section>
</template>
<style scoped>
.encabezado{
    display: flex;
    align-items: center;
    margin-bottom: 20px;
}
.encabezado h4, h5{
    font-weight: bold;
    font-size: .9rem;
    margin-bottom: 0;
}
.encabezado i {
    font-size: 1.5rem;
margin: 0 3px 0 15px;
}
.color {
    background-color: green;
    color: white;
}
.noColor {
    background-color: transparent;
    color: black;
}
.tiempo{
    position: absolute;
    top: 33%;
    right: 8%;
    background-color: rgba(0, 0, 0, 0.748);
    color: white;
    padding: 5px;
    border-radius: 15%;
}
/* .wrapper .carousel {
    display: grid;
    grid-auto-flow: column;
    grid-auto-columns: calc((100% / 4) - 12px);
    gap: 16px;
    /* overflow: hidden; */
/* }
.carousel {
    z-index: -1;
}
.wrapper {
    max-width: 1100px;
    width: 100%;
    position: relative !important;
} */
/* .wrapper i {
    height: 50px;
    width: 50px;
    background-color: white;
    text-align: center;
    line-height: 50px;
    border-radius: 50%;
    cursor: pointer;
    position: absolute !important;
    top: 50%;
    font-size: 1.25rem;
    transform: translateY(-50%);
    box-shadow: 0 3px 6px rgba(0, 0, 0, .23);
    z-index: 999;
}
.wrapper i:first-child {
    left: -22px;
}
.wrapper i:last-child {
    right: -22px;
}  */
.card-body h5, p {
    margin: 0;
    padding-top: 3px;
}
.card-body h5 {
    width: 90%;
    font-size: .9rem;
}
</style>