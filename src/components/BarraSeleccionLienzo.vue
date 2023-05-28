<script setup>
import { colocarValorNombreLienzo } from './OpcionesElemento.vue'

function agregarLienzo() {

    const barraSeleccion = document.getElementById("seleccionLienzo")

    let nuevoLienzo = document.createElement("div")
    nuevoLienzo.className = "contenedor"
    nuevoLienzo.innerHTML = '<div class="lienzo"></div>'
    document.getElementById("contenedorLienzos").appendChild(nuevoLienzo)

    let btnSeleccionLienzo = document.createElement("button")
    btnSeleccionLienzo.classList.add("boton-lienzo", "boton-activo")
    btnSeleccionLienzo.value = barraSeleccion.childNodes.length
    btnSeleccionLienzo.textContent = "Lienzo " + btnSeleccionLienzo.value.toString()
    btnSeleccionLienzo.addEventListener("click", () => {
        
        let elementoSeleccionado = document.getElementsByClassName("seleccionado")[0]
        if(elementoSeleccionado) elementoSeleccionado.classList.remove("seleccionado")
        
        cargarLienzo(btnSeleccionLienzo)
    })
    barraSeleccion.appendChild(btnSeleccionLienzo)
    cargarLienzo(btnSeleccionLienzo)
}

function borrarLienzo(){

    const barraSeleccion = document.getElementById("seleccionLienzo")
    if(!barraSeleccion) return
    const contenedorLienzos = document.getElementById("contenedorLienzos")
    if(!contenedorLienzos) return
    const btnActico = document.getElementsByClassName("boton-activo")
    if (!btnActico) return
    const lienzoActivo = document.getElementsByClassName("activo")
    if (!lienzoActivo) return

    barraSeleccion.removeChild(btnActico[0])
    contenedorLienzos.removeChild(lienzoActivo[0])
    
    const seleccionNueva = barraSeleccion.childNodes[barraSeleccion.childNodes.length-1]

    seleccionNueva.classList.add("boton-activo")
    document.getElementsByClassName("contenedor")[seleccionNueva.value-1].classList.add("activo")
    colocarValorNombreLienzo(seleccionNueva.textContent)
}
</script>

<script>

export function cargarLienzo(btnSeleccionLienzo){
    marcaBotonLienzoActivo(btnSeleccionLienzo)
    mostrarLienzo(btnSeleccionLienzo.value - 1)
    colocarValorNombreLienzo(btnSeleccionLienzo.textContent)
}

export function mostrarLienzo(indice) {

    let lienzoEnPantalla = document.getElementsByClassName("activo")
    lienzoEnPantalla[0].classList.remove("activo")

    let lienzos = document.getElementsByClassName("contenedor")
    lienzos[indice].classList.add("activo")
}

export function marcaBotonLienzoActivo(boton) {
    let btnLienzoActivo = document.getElementsByClassName("boton-activo")
    if (btnLienzoActivo !== undefined) btnLienzoActivo[0].classList.remove("boton-activo");

    boton.classList.add("boton-activo")
}

export function definnirNombreLienzo(nuevoNombre) {
    let btnLienzoActivo = document.getElementsByClassName("boton-activo")
    btnLienzoActivo[0].textContent = nuevoNombre
}

export function obtenerNombreLienzo(){
    let btnLienzoActivo = document.getElementsByClassName("boton-activo")
    return btnLienzoActivo[0].textContent
}


</script>

<template>
    <div id="seleccionLienzo" class="seleccionLienzo">
        <div class="accionesLienzo">
            <v-btn id="btnAgregarLienzo" class="btnAgregarLienzo" icon="mdi-plus" @click="agregarLienzo()" style=" width: calc(var(--v-btn-height) + 5px);
    height: calc(var(--v-btn-height) + 5px); margin: 2%;"></v-btn>
            <v-btn id="btnEliminarLienzo" class="btnEliminarLienzo" icon="mdi-delete" style=" width: calc(var(--v-btn-height) + 5px);
    height: calc(var(--v-btn-height) + 5px); margin: 2%;" @click="borrarLienzo()" ></v-btn>
        </div>
    </div>
</template>

<style scoped>

.seleccionLienzo {
    left: 0;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100px;
    background-color: #ecf8f2;
}

.accionesLienzo {
    display: flex;
    position: absolute;
    bottom: 20px;
    left: 45px;
    transform: translate(-50%);
    color: white;
}

.btnAgregarLienzo{
    background: #afd28d;
}

.btnEliminarLienzo{
    background: #f24265;
}
</style>
<style>
.boton-lienzo {
    width: 100%;
    height: 5%;
    margin: 10px;
    border-style: none;
    background: #b08dd2;
    color: aliceblue;
}

.boton-activo {
    box-shadow: 0 0 3px 1px #1560e1;
    outline: none;
}

</style>