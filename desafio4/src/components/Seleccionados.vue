<script setup>
import { ref, watch, onMounted } from 'vue';
//Variables para recibir datos del TemplateRef
const nombreVideo = ref(null);
console.log(nombreVideo.value);
const listaNombres = ref([]);

//Variables para recibir los datos por Props
const props = defineProps({
    videoName2: Array,
  });

onMounted(()=>{
    //Ejecutar cuando se monta el Componente
     console.log('Componente Montado');
  // console.log(`antes del watch esperando el props ${props.videoName}`);

})
/**
 * Funcion para recibir por TemplateRef nombre de card de video seleccionada en el Componente Padre
 */
function addStringToChildComponent() {
  // Check if the input string is already in the array
  if (!listaNombres.value.includes(nombreVideo.value) && nombreVideo.value!==null) {
    listaNombres.value.push(nombreVideo.value)
    console.log("en la funcion para agregar el nombre del video");
    console.log(`en la funcion para agregar el nombre del video : nombre ${listaNombres.value}`);

    nombreVideo.value = null
  }
}
function updateInputString(value) {
  nombreVideo.value = value
}
defineExpose({
  addStringToChildComponent,
  updateInputString,
})
const emit = defineEmits(['remove-video']);
function removeVideo(video2) {
  emit("remove-video", video2);
}
onMounted(() => {
  console.log(`en onMounted del hijo ${nombreVideo.value}`);
  /**
   * Vigilar por medio de watch la variable donde se recibe el nombre del video que se dio click y validar si el mismo ya existe para eliminarlo de la lista
   */
  watch(nombreVideo,  () => {
    console.log("en el watch");
    console.log(listaNombres.value);
    console.log("dentro del if del watch");
    if (listaNombres.value.includes(nombreVideo.value) && !nombreVideo.value!==null) {
   //eliminar del arreglo solo el nombre seleccionado
   const index = listaNombres.value.indexOf(nombreVideo.value);
     listaNombres.value.splice(index, 1);
     console.log("elemento existe, se ha eliminado");
     nombreVideo.value = null
  }
    console.log("luego el if del watch");
    console.log(listaNombres.value);
    console.log("elemento existe, se ha eliminado");
    console.log(nombreVideo.value);
    })
  });
</script>

<template>
    <div  class="seleccionados">
    <div v-if="listaNombres.length > 0">
      <h2 class="titulo">Lista Refs</h2>
      <ul class="lista-refs">
        <li v-for="(video, idx) in listaNombres" :key="idx">
          {{ video }}
        </li>
      </ul>
    </div>
    <hr v-if="props.videoName2.length > 0">
    <div v-if="props.videoName2.length > 0">
      <h2 class="titulo">Lista Props</h2>
      <ul class="lista-props">
         <li v-for="(video2, index) in props.videoName2" :key="index" @click="removeVideo(video2)">
          {{ video2 }}
        </li>
      </ul>
    </div>
    </div>
  </template>

  <style scoped>
  .seleccionados {
    padding: 10px;
    margin-top: 10px;
    position: absolute;
    width:  23%;
    right: 0;
    top: 800px;
  }
  </style>