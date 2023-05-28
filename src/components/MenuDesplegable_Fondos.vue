<script setup>

import Fondo1 from "../assets/Fondos/Fondo1.jpg"
import Fondo2 from "../assets/Fondos/Fondo2.jpg"
import Fondo3 from "../assets/Fondos/Fondo3.jpg"
import Fondo4 from "../assets/Fondos/Fondo4.jpg"
import Fondo5 from "../assets/Fondos/Fondo5.jpg"
import Fondo6 from "../assets/Fondos/Fondo6.jpg"
import Fondo7 from "../assets/Fondos/Fondo7.jpg"
import Fondo8 from "../assets/Fondos/Fondo8.jpg"

const listaImagenes = [{ id: "E_F_1", imagen: Fondo1 }, { id: "E_F_2", imagen: Fondo2 },{id:"E_F_3", imagen: Fondo3},
                        { id: "E_F_4", imagen: Fondo4 }, { id: "E_F_5", imagen: Fondo5 },{id:"E_F_6", imagen: Fondo6},
                        { id: "E_F_7", imagen: Fondo7 }, { id: "E_F_8", imagen: Fondo8 },
                    ]

function ponerImagen (e, listaImagenes) {

    const canvas = document.getElementsByClassName("activo")
    const imagenSelecMenu = e.target

    const imagenSelec = listaImagenes.find(img => imagenSelecMenu.id === img.id)
    
    canvas[0].childNodes[0].style = 'background-image : url(' + imagenSelec.imagen + '); background-size: cover; background-repeat: no-repeat;'
}

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
                <v-btn class="botonMenuDesplegable"  v-bind="props"> Fondos</v-btn>
            </template>

            <v-card max-width="350" max-height="500">
                <img type="button" v-for="imagenFondo in listaImagenes" :id="imagenFondo.id" :src="imagenFondo.imagen" class="imagenIcono" 
                draggable="true" alt="" @click="ponerImagen($event, listaImagenes)" />
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