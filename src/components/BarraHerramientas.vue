<script setup>
import MenuDesplegable_Dialogos from "./MenuDesplegable_Dialogos.vue";
import MenuDesplegable_Fondos from "./MenuDesplegable_Fondos.vue";
import MenuDesplegable_Personajes from "./MenuDesplegable_Personajes.vue";
</script>

<script>
export function cambiarTamanio(scala) {

  const elementoSeleccionado = document.getElementsByClassName("seleccionado")
  if (!elementoSeleccionado[0]) return;

  let posicion = { left: elementoSeleccionado[0].style.left, top: elementoSeleccionado[0].style.top }
  elementoSeleccionado[0].style = 'left: ' + posicion.left + '; top: ' + posicion.top + '; transform: scale(' + scala + ');'
}

export function seleccionElemento(elementoSelecionado) {
    let seleccionado = document.getElementsByClassName("seleccionado")
    if (seleccionado[0]) {
        seleccionado[0].classList.remove("seleccionado")
        elementoSelecionado.classList.add("seleccionado")
    } else {
        elementoSelecionado.classList.add("seleccionado")
    }
}
</script>

<template>
  <v-toolbar color="#5B2391" location="top" width="auto">

    <MenuDesplegable_Personajes/>
    <MenuDesplegable_Fondos />
    <MenuDesplegable_Dialogos />

    <v-spacer></v-spacer>

    <v-toolbar-title class="titulo" text="Proyect S-Draw"></v-toolbar-title>
  </v-toolbar>
</template>
<style scoped>
.titulo {
  margin-inline-end: 16px;
  text-align: right;
  color: aliceblue;
  /*Cambiar fuente*/
}
</style>

<style>
.imagenIcono {
  margin: 10px;
  width: 80px;
  height: 80px;
}

.imagenIcono:hover{
    box-shadow: 0 0 3px 2px #8AB278;
    outline: none;
}

.seleccionado {
  border: 3px;
  border-color: #9060C0;
  border-radius: 5px;
  box-shadow: 0 0 4px 3px #A077C9;
  outline: none;
  z-index: 10000;
}
</style>