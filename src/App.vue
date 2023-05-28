<script setup>
import BarraHerramientas from './components/BarraHerramientas.vue';
import OpcionesElemento from './components/OpcionesElemento.vue';
import BarraSeleccionLienzo, { cargarLienzo, definnirNombreLienzo } from './components/BarraSeleccionLienzo.vue';
import { cambiarTamanio } from './components/BarraHerramientas.vue';

window.onload = () => {
  const lienzos = document.getElementsByClassName("contenedor")
  const barraSeleccion = document.getElementById("seleccionLienzo")

  for (let indexLienzo = 0; indexLienzo < lienzos.length; indexLienzo++) {

    let btnSeleccionLienzo = document.createElement("button")
    btnSeleccionLienzo.classList.add("boton-lienzo", "boton-activo")
    btnSeleccionLienzo.value = indexLienzo + 1
    btnSeleccionLienzo.textContent = "Lienzo " + btnSeleccionLienzo.value.toString()
    btnSeleccionLienzo.addEventListener("click", () => {

      let elementoSeleccionado = document.getElementsByClassName("seleccionado")[0]
      if (elementoSeleccionado) elementoSeleccionado.classList.remove("seleccionado")

      cargarLienzo(btnSeleccionLienzo)
    })
    barraSeleccion.appendChild(btnSeleccionLienzo)
    cargarLienzo(btnSeleccionLienzo)
  }

  const sliderTamanio = document.getElementById("sliderTamanio")
  const textoTamanio = document.getElementById("tamanioElemento")

  sliderTamanio.style.backgroundSize = (sliderTamanio.value - sliderTamanio.min) * 100 / (sliderTamanio.max - sliderTamanio.min) + '% 100%'

  sliderTamanio.addEventListener("input", () => {

    textoTamanio.value = Math.round(sliderTamanio.value * 100)
    sliderTamanio.style.backgroundSize = (sliderTamanio.value - sliderTamanio.min) * 100 / (sliderTamanio.max - sliderTamanio.min) + '% 100%'
    cambiarTamanio(sliderTamanio.value)
  })

  textoTamanio.addEventListener("input", () => {
    sliderTamanio.value = textoTamanio.value / 100
    sliderTamanio.style.backgroundSize = (sliderTamanio.value - sliderTamanio.min) * 100 / (sliderTamanio.max - sliderTamanio.min) + '% 100%'
    cambiarTamanio(sliderTamanio.value)
  })

  const inputNombreLienzo = document.getElementById("nombreLienzo")
  inputNombreLienzo.addEventListener("input", () => {
    definnirNombreLienzo(inputNombreLienzo.value)
  })
  inputNombreLienzo.addEventListener("keydown",(e)=>{
    if(e.key=='Enter') inputNombreLienzo.blur()
  })
}

function removerSelecionElemento() {

  let seleccionado = document.getElementsByClassName("seleccionado")[0]
  if (seleccionado) seleccionado.classList.remove("seleccionado")

}

</script>

<template>
  <v-app>
    <!--Barra de herramientas y titulo de la app -->
    <div class="Titulo">
      <BarraHerramientas />
      <OpcionesElemento tamanio="1" />
    </div>
    <!--Lienzo para hacer el dibujo-->
    <div id="presentacion" class="presentacion">
      <BarraSeleccionLienzo />
      <div id="contenedorLienzos" class="contenedorLienzos">
        <div id="contenedor" class="contenedor activo">
          <div id="lienzo" class="lienzo"></div>
        </div>
      </div>
    </div>
  </v-app>
</template>

<style scoped>
.presentacion {
  display: flex;
  flex-direction: row;
  height: 100%;
  width: auto;
}

.contenedorLienzos {
  display: flex;
  flex: 1;
  flex-direction: column;
  align-items: center;
  background-color: #e0e6e4;
}


.Titulo {
  position: sticky;
  top: 0;
  height: max-content;
  z-index: 1;
}
</style>

<style>
.elementoEnCanvas {
  position: absolute;
  width: 7em;
  height: auto;
  top: 50%;
  left: 50%;
  cursor: move;
}

.contenedor {
  display: none;
  align-self: center;
  height: auto;
  width: auto;
}

.lienzo {
  display: flex;
  height: 480px;
  width: 720px;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -25%);
  background: #ffffffa3;
}

.activo {
  display: flex;
}

textarea{
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-size: x-small;
}
</style>