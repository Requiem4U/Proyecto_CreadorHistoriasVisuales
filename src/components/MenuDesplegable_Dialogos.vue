<script setup>

import { seleccionElemento } from "./BarraHerramientas.vue";

import CD1 from "../assets/Dialogos/Dialogo1.png"
import CD2 from "../assets/Dialogos/Dialogo2.png"
import CD3 from "../assets/Dialogos/Dialogo3.png"
import CD4 from "../assets/Dialogos/Dialogo4.png"
import CD5 from "../assets/Dialogos/Dialogo5.png"
import CD6 from "../assets/Dialogos/Dialogo6.png"

const listaImagenes = [{ id: "E_D_1", imagen: CD1 }, {id:"E_D_2", imagen: CD2}, {id:"E_D_3", imagen: CD3},
                        { id: "E_D_4", imagen: CD4 }, {id:"E_D_5", imagen: CD5}, {id:"E_D_6", imagen: CD6},
                    ]


const textAreaHTML = '<div class="v-textarea--auto-grow">'
                    + '   <textarea class="v-field__input" style="margin: 10px; padding: 1%;"></textarea>'
                    + '</div>'

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

    const textArea = document.createElement('textarea');
    textArea.setAttribute("maxlength","10")
    textArea.classList.add("dialogo")
    textArea.style = 'background-image : url(' + imagenSelec.imagen + '); background-size: contain; background-repeat: no-repeat;'
    

    textArea.addEventListener("mousedown", (e) => {

        seleccionElemento(textArea)

        Xinicial = e.clientX
        Yinicial = e.clientY

        moverElemento = true
    })

    textArea.addEventListener("mousemove", (e) => {
        if (!moverElemento) return;
        let nuevaX = e.clientX
        let nuevaY = e.clientY

        textArea.style.top = textArea.offsetTop - (Yinicial - nuevaY) + "px"
        textArea.style.left = textArea.offsetLeft - (Xinicial - nuevaX) + "px"

        Xinicial = nuevaX
        Yinicial = nuevaY
    })

    const elementoNuevo = document.createElement("div")
    elementoNuevo.appendChild(textArea)
    elementoNuevo.className = "elementoEnCanvas"

    canvas[0].appendChild(elementoNuevo)
}

window.addEventListener("mouseup", () => {
    moverElemento = false
})

</script>

<script>
export default {
    data() {
        return {
            menu: false
        };
    },
};
</script>


<template>
    <div class="text-center">
        <v-menu v-model="menu" :close-on-content-click="true" location="bottom center">
            <template v-slot:activator="{ props }">
                <v-btn class="botonMenuDesplegable" v-bind="props"> Diálogos </v-btn>
            </template>

            <v-card max-width="350" max-height="500">
                <img type="button" v-for="imagenDialogo in listaImagenes" :id="imagenDialogo.id" :src="imagenDialogo.imagen"
                    class="imagenIcono" draggable="true" alt="" @click="ponerImagen($event, listaImagenes)" />
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
.dialogo{
    width: 100px;
    height: 100px;
    resize: none;
    padding:15px;
    overflow: hidden;
    font-family: 'Courier New', Courier, monospace;
    font-size: small;
}
</style>