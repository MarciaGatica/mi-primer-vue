
<!--   logica   -->
<script setup>
import { ref, computed } from 'vue'


const claseCounter = computed(() => {
  if (cont.value === 0) {
    return 'cero'
  }
  if (cont.value > 0) {
    return 'positivo'
  }
  if (cont.value < 0) {
    return 'negativo'
  }
});



//metodo - methods --> una funcion es un metodo
const presionar = (mensaje) => {
  console.log(mensaje)
}


const cont = ref(0); // ref --> variable reactiva, para que sea dinamica y cambie

const favorito = ref([]);

const incrementar = () => {
  cont.value++; //solo se puede modificar en el script
}

const disminuir = () => {
  cont.value--; //solo se puede modificar en el script
}

const resetear = () => {
  cont.value = 0; //solo se puede modificar en el script
}


const agregar = () => {
  favorito.value.push(cont.value); //push empujar variable es como el add
}

const blokearBtnAgregar = computed(() => {
  const buscarNum = favorito.value.find((num) => num === cont.value);
  return buscarNum || buscarNum === 0; //si existe returna verdadero, pero el 0 siempre es falso por eso la condicion
})
</script>




<!-- Estructura -->
<template>
  <div class="container text-center mt-3"> <!-- mt = margin top -->
    <button v-on:click="presionar('click 1')">Activame 1</button>
    <button @click="presionar('click 2')">Activame 2</button> <!-- v-on es lo mismo que el @ -->



    <!-- Detectar que btn del mause se esta presionando -->
    <button @click.left="presionar('click izquierdo')">izquierdo</button>
    <button @click.right="presionar('click derecho')">derecho</button>
    <button @click.middle="presionar('click central')">central</button>



    <!-- btns que modifican el numero en tiempo real -->
    <h2 v-if="cont < 0" style="color: red;">Modo a: {{ cont }}</h2>
    <h2 v-else style="color: green;">Modo a: {{ cont }}</h2>


    <!-- modo 2 -->
    <h2 :class="cont >= 0 ? 'positivo' : 'negativo'">Modo b: {{ cont }}</h2>

    <!-- modo 3 -->
    <h2 :class="claseCounter">Modo c: {{ cont }}</h2>
    <div class="btn-group">
      <button @click="disminuir" class="btn btn-danger">
        Disminuir</button>
      <button @click="resetear" class="btn btn-secondary">
        Resetear</button>
      <button @click="incrementar" class="btn btn-success">
        Aumentar</button>

      <button @click="agregar" :disabled="blokearBtnAgregar" class="btn btn-primary">
        agregar</button>

    </div>



    <h2>Favorito: {{ favorito }}
      <ul class="list-group">
        <li v-for="(num, index) in favorito" :key="index" class="list-group-item ">  
          {{ num }}
        </li>
      </ul>
    </h2>

  </div>
</template>




<!--   estilos    -->          
<style>
.positivo {
  color: green;
}

.negativo {
  color: red;
}

.cero {
  color: peru;
}
</style>