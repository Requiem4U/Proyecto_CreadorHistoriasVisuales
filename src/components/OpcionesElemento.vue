<script setup>

defineProps({
    tamanio: Number
})

</script>

<script>
export function colocarValorNombreLienzo(nombre){
    const inputNombreLienzo = document.getElementById("nombreLienzo")
    inputNombreLienzo.value = nombre
}

</script>

<template>
    <div class="barraOpcionesElemento">
        <input type="text" id="nombreLienzo" maxlength="13">
        <input type="range" id="sliderTamanio" max="2" min="0.5" :value="tamanio" step="0.01">
        <input id="tamanioElemento" type="number" :value="Math.round(tamanio * 100)" max="300" min="10">
        
    </div>
</template>

<style scoped>
.barraOpcionesElemento {
    display: flex;
    flex-flow: row;
    width: max-content;
    height: 50px;
    left: 15px;
}

input:focus {
    box-shadow: 0 0 3px 3px #8AB278;
    outline: none;
}

input[type="text"]{
    background-color: #e7e6e6c3;
    margin: 5px;
    border-radius: 5px;
    text-align: center;
}

input[type="number"]{
    background-color: #e3e2e2;
    margin: 5px;
    border-radius: 5px;
    text-align: center;
    width: 60px;
}

input[type="range"] {
    -webkit-appearance: none;
    align-self: center;
    margin-left: 5%;
    margin-right: 15px;
    width: 200px;
    height: 10px;
    background: #DECFEC;
    border-radius: 5px;
    background-image: linear-gradient(to right, #BC9EDA, #703F9F);
    background-size: 30% 100%;
    background-repeat: no-repeat;
}

input[type=range]::-webkit-slider-runnable-track {
    -webkit-appearance: none;
    box-shadow: none;
    border: none;
    background: transparent;
}

input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    height: 20px;
    width: 20px;
    border-radius: 50%;
    background: #441201;
    cursor: ew-resize;
    box-shadow: 0 0 2px 0 #555;
    transition: background .3s ease-in-out;
}

span {
    width: min-content;
    margin: 0 0 0 15px;
    padding: 2px 7px;
    font-size: medium;
    font-family: sans-serif;
    background-color: darkgray;
}
</style>