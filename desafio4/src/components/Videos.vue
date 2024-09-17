<script setup>
import { computed, ref, onMounted, watch } from 'vue';
import videosData from '../dataBase/videos.json';
import Seleccionados from './Seleccionados.vue';
// core version + navigation, pagination modules:
import { Swiper } from 'swiper';
// import { Navigation, Pagination } from "swiper/modules";
// import Swiper and modules styles
import 'swiper/css';
import 'swiper/css/navigation';
import 'swiper/css/pagination';
//se agregan los datos del arreglo de videos.json a una nueva variables para la lectura de datos en las cards
let vds = ref([]);
vds = videosData.videos;
console.log(vds);
console.log("en componente videos");
console.log(vds.title)
const videoSeleccionado = ref(null);
const idSeleccionado = ref([]);
const idSeleccionado2 = ref([]);
const videoName2 = ref([]);
const videoId = ref([]);

console.log(`video seleccionado inicio ${idSeleccionado}`);
//logica para mandar por TemplateRef nombre de la card seleccionada al componente hijo Seleccionados.vue
const seleccionadosRef = ref(null);
function agregarNombreSeleccionado(video){
  console.log(`lo que recibe la funcion para enviar al templateRef ${video}`);
  console.log("en la constante para agregar dato al templateRef");
  console.log(`selecionadosRef : ${seleccionadosRef.value}`);
  console.log(`selecionadosRef value nombreVideo : ${seleccionadosRef.value.nombreVideo}`);
if (seleccionadosRef.value) {
  seleccionadosRef.value.updateInputString(video);
  seleccionadosRef.value.addStringToChildComponent()
} 
}
/** 
*Logica para enviar por Props video seleccionado de la seccion 2 de cards
**/
function nombre2(nombre, id) {
  console.log("en variable nombre del segundo arreglo");
  console.log(videoName2.value);
  if (!videoName2.value.includes(nombre + ".")) {
  videoName2.value.push(nombre + ".");
  }
  const index = idSeleccionado2.value.indexOf(id);
     if (!index > -1) {
   //sino lo agregamos a la lista
   idSeleccionado2.value.push(id);
    console.log("en funcion");
    console.log(id);
    console.log(this.elements);
      const element = document.getElementById(id);
      console.log("luego de la constante");
      console.log(element);
      element.style.backgroundColor = "green"; // Change to desired color
console.log(`video seleccionado cargado ${idSeleccionado2.value.length}`);

     }
}
console.log("despues de funcion de agregar vriable nombre del segundo arreglo");

   //cambiar background-color al div del videoSeleccionado
   function changeColor(id) {
    //conseguir elemento id dentro del arreglo idSeleccionado
    const index = idSeleccionado.value.indexOf(id);
     if (index > -1) {
       //si esta en la lista lo eliminamos
      idSeleccionado.value.splice(index, 1);
      const element2 = document.getElementById(id);
      element2.style.backgroundColor = "white"; // Change to desired color
console.log(`video seleccionado quitado ${idSeleccionado.value.length}`);

     } else {
        //sino lo agregamos a la lista
       idSeleccionado.value.push(id);
    console.log("en funcion");
    console.log(id);
    console.log(this.elements);
      const element = document.getElementById(id);
      console.log("luego de la constante");
      console.log(element);
      element.style.backgroundColor = "green"; // Change to desired color
console.log(`video seleccionado cargado ${idSeleccionado.value.length}`);
      console.log(isSelectionActive.value);
    };
  };
// consultar video seleccionado para crear una computada que indique si se ha seleccionado un video
  function seleccionarVideo(idVideo) {
    console.log(`video seleccionado ${idVideo}`);
  videoSeleccionado.value = idVideo;
  console.log(videoSeleccionado.value.length);  
};
const isSelectionActive = computed(() => {
  if (videoSeleccionado.value === null) {
    return "seleccion inactiva";
  } else {
    return "seleccion activa";
  }
});
//prueba onMounted
onMounted(() => {
    console.warn('Evento onMounted disparado en Videos.vue');
    console.log(isSelectionActive.value);
    console.log(swiper); 
})
/**
 * funcion carousel
*/
function removeVideoFromList(video2) {
  const index = videoName2.value.indexOf(video2);
  const index2 = idSeleccionado2.value.indexOf(video2);
  if (index!== -1) {
    videoName2.value.splice(index, 1);
    if (index2 > -1) {
      const cambiar = document.getElementById(video2);
      cambiar.style.backgroundColor = "white";
   idSeleccionado2.value.slice(video2, 1);
    }
     }
  
}
var swiper = new Swiper(".mySwiper", {
  // Optional parameters
  direction: "vertical",
  loop: true,
// If we need pagination
pagination: {
    el: ".swiper-pagination",
  },
  // Navigation arrows
  navigation: {
    nextEl: ".swiper-button-next",
    prevEl: ".swiper-button-prev",
  },

  // And if we need scrollbar
  scrollbar: {
    el: ".swiper-scrollbar",
  },
});
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
          <div class="swiper mySwiper">
    <!-- Additional required wrapper -->
      <!-- Slides -->
      <div :class="{ selected: isSelectionActive }" class="swiper-wrapper gap-1 " style="width: 90%;" >
                      <div v-for="(videos, idx) in vds" :key="idx" :id="idx" @click="seleccionarVideo(idx), changeColor(idx), agregarNombreSeleccionado(videos.title)" class="swiper-slide card col-sm-3 mb-3 mb-sm-0" style="border: none; width: 13rem; height: auto;">
                    <img :src="videos.urlImg" class="card-img" style="width: 97%; height: 7rem;" alt="...">
                    <h5 class="tiempo">{{ videos.duration }}</h5>
                    <div class="card-body px-0">
                      <h5 class="card-title">{{ videos.title }}</h5>
                      <p class="card-text">CADI F1 C.A.</p>
                      <p class="card-text">{{ videos.views }} visualizaciones</p>
                      <p class="card-text">· Emitido hace {{ idx + 1 }} semanas</p>
                    </div> 
                  </div>
              </div>
     <!-- If we need navigation buttons -->
    <div @click="swiper.slidePrev()" class="swiper-button-prev"></div>
    <div @click="swiper.slideNext()" class="swiper-button-next"></div>
  </div>
          <hr>
          <div class="encabezado">
              <h4>Carreras Tecnicas</h4>
              <i class="bi bi-caret-right"></i>
              <h5>Reproducir todo</h5>
          </div>
         <!-- Slider main container -->
  <div class="swiper mySwiper">
    <!-- Additional required wrapper -->
      <!-- Slides -->
      <div :class="{ selected: isSelectionActive }" class="swiper-wrapper gap-1 " >
                      <div v-for="(videos, idx) in vds" :key="idx+21" :id='(videos.title+".")' @click='seleccionarVideo(idx+21), nombre2(videos.title, (videos.title+"."))' class="swiper-slide card col-sm-3 mb-3 mb-sm-0" style="border: none; width: 13rem; height: auto;">
                    <img :src="videos.urlImg" class="card-img" style="width: 97%; height: 7rem;" alt="...">
                    <h5 class="tiempo">{{ videos.duration }}</h5>
                    <div class="card-body px-0">
                      <h5 class="card-title">{{ videos.title }}.</h5>
                      <p class="card-text">CADI F1 C.A.</p>
                      <p class="card-text">{{ videos.views }} visualizaciones</p>
                      <p class="card-text">· Emitido hace {{ idx + 22 }} semanas</p>
                    </div> 
                  </div>
              </div>
     <!-- If we need navigation buttons -->
    <div @click="swiper.slidePrev()" class="swiper-button-prev"></div>
    <div @click="swiper.slideNext()" class="swiper-button-next"></div>
  </div>
<Seleccionados ref="seleccionadosRef" :videoName2="videoName2" :videoID="videoId" @remove-video="removeVideoFromList"/>
    </section>
</template>
<style scoped>
.swiper-button-prev {
  color: rgba(0, 0, 0, 0.938);
  height: 40px !important;
    width: 40px !important;
    background-color: rgba(255, 255, 255, 0.723);
    text-align: center;
    border-radius: 50%;
    padding: 5px;
}
.swiper-button-prev:after {
  font-size: 1.2rem !important; 
}
.swiper-button-next {
  color: rgba(0, 0, 0, 0.938);
  height: 40px !important;
    width: 40px !important;
    background-color: rgba(255, 255, 255, 0.723);
    text-align: center;
    font-size: .4rem !important;
    border-radius: 50%;
    padding: 5px;
}
.swiper-button-next:after { 
  font-size: 1.2rem !important; 
}
.swiper {
  width: 80% !important;
  margin-left: 0;
}
hr {
  width: 80% !important;
}
.card {
    display: flex;
    align-items: center;
}
.swiper {
      width: 100%;
      height: 100%;
    }
.encabezado {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
}
.encabezado h4, h5 {
    font-weight: bold;
    font-size: .9rem;
    margin-bottom: 0;
}
.encabezado i {
    font-size: 1.5rem;
margin: 0 3px 0 15px;
}
.tiempo {
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