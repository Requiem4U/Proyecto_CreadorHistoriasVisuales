<script>
export default {
    data() {
        return {
            menu: false
        };
    },
};
</script>

<script setup>

import { seleccionElemento } from "./BarraHerramientas.vue";

import P1 from "../assets/Personajes/Chef1.png"
import P2 from "../assets/Personajes/Mesero1.png"
import P3 from "../assets/Personajes/Mesero2.png"

const listaImagenes = [{ id: "E_F_1", imagen: P1 }, { id: "E_F_2", imagen: P2 }, { id: "E_F_3", imagen: P3 },

]


let moverElemento = false;

function ponerImagen(e, listaImagenes) {

    let Xinicial = 0;
    let Yinicial = 0;

    const canvas = document.getElementsByClassName("activo")
    const canvasRect = canvas[0].getBoundingClientRect()
    const imagenSelecMenu = e.target

    const imagenADibujar = new Image()
    const imagenSelec = listaImagenes.find(img => imagenSelecMenu.id === img.id)
    imagenADibujar.src = imagenSelec ? imagenSelec.imagen : "";
    imagenADibujar.className = "elementoEnCanvas"

    imagenADibujar.addEventListener("mousedown", (e) => {
        e.preventDefault()

        seleccionElemento(imagenADibujar)

        Xinicial = e.clientX
        Yinicial = e.clientY

        moverElemento = true
    })

    imagenADibujar.addEventListener("mousemove", (e) => {
        if (!moverElemento) return;
        e.preventDefault()
        let nuevaX = e.clientX
        let nuevaY = e.clientY

        imagenADibujar.style.top = imagenADibujar.offsetTop - (Yinicial - nuevaY) + "px"
        imagenADibujar.style.left = imagenADibujar.offsetLeft - (Xinicial - nuevaX) + "px"

        Xinicial = nuevaX
        Yinicial = nuevaY
    })

    const elementoNuevo = document.createElement("div")
    elementoNuevo.appendChild(imagenADibujar)
    elementoNuevo.className = "elementoEnCanvas"

    canvas[0].appendChild(elementoNuevo)
}

window.addEventListener("mouseup", () => {
    moverElemento = false
})

</script>

<template>
    <div class="text-center">
        <v-menu v-model="menu" :close-on-content-click="true" location="bottom center">
            <template v-slot:activator="{ props }">
                <v-btn class="botonMenuDesplegable" v-bind="props"> Personajes </v-btn>
            </template>

            <v-card max-width="350" max-height="500">
                <img type="button" v-for="ruta in listaImagenes" :id="ruta.id" :src="ruta.imagen"
                    class="imagenIconoPersonaje" draggable="true" alt="" @click="ponerImagen($event, listaImagenes)" />
            </v-card>
        </v-menu>
    </div>
</template>

<style scoped>
.botonMenuDesplegable {
    font-family: Arial, Helvetica, sans-serif;
    color: aliceblue;
}
</style>
<style>
.imagenIconoPersonaje {
    margin: 10px;
    width: 50px;
    height: 80px;
}

.imagenIconoPersonaje:hover{
    box-shadow: 0 0 3px 2px #8AB278;
    outline: none;
}
</style>