<script setup>
/*Documentacion
https://www.youtube.com/watch?v=PL-aTHv2L3E&list=PLPl81lqbj-4J-gfAERGDCdOQtVgRhSvIT
https://bluuweb.github.io/vue-udemy/30-01-fundamentos/#v-for
*/
//Para renderizar 
import {ref, computed} from 'vue'
const counter = ref(0);
const arrayFavoritos = ref([])
const increment = () => {
  //console.log("aumentar contador");
  counter.value ++;
 // console.log(counter);
};
const decrement = () => counter.value --

const reset = () => (counter.value = 0);

const add = () => {
  arrayFavoritos.value.push(counter.value)
}

const bloquearBtnAdd = computed(() =>{
  const numSearch = arrayFavoritos.value.find((num) => num === counter.value);
  console.log(numSearch);
  if(numSearch === 0) return true;
  return numSearch ? true : false;
  //return numSearch || numSearch === 0
});

const classCounter = computed(() => {
  if(counter.value === 0){
    return 'zero'
  }
  if(counter.value > 0){
    return 'positive'
  }
  if(counter.value < 0){
    return 'negative'
  }
})
//
  const name = "Vue dinamico";

  const styleColor = "color: blue"
  const arrayColores = ["blue","red","peru"];
  const activo = false;
  /*const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];*/
  const arrayFrutas1 = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
        },
    ];

    const arrayFrutas = [
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
            stock : 0,
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
            stock : 10,
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
            stock : 20,
        },
    ];
  
  const objetoFruta = {
    name: "Manzana",
    price:"$1.0",
    description: "Una manzana",
    id: 1,
  };

//Eventos
  const handleClick = (message) => {
    console.log(message)
  }
  //Renderizar contador
</script>
<template>
  <div class="container">

  
  <h1>Hola {{ name.toUpperCase() }}</h1>
  <br>
  <h2>{{ arrayColores }}</h2>
  <br>
  <h2 :style=" `color: ${arrayColores[2]}`">Soy peru</h2>
  <br>
  <h2 v-if="activo === true">
    <span> Icono</span>
    Estoy activo
  </h2>
  <p v-else-if="activo ===false">Estoy inactivo</p>
  <p v-else>Estoy indeciso</p>

  <h2 v-show="activo">Estoy activo v-show</h2>
  <br>
  <h2>Arreglo:</h2>
  <br>
  <ul>
        <li v-for="fruta in arrayFrutas1" :key="fruta.name">
           {{ fruta.name }} - {{ fruta.price }} - {{ fruta.description }}
        </li>
    </ul>
    <br>
    <h2>Objeto:</h2>
  <br>
    <ul>
      <li v-for="(value, propiedad, index) of objetoFruta" :key="index">
       {{ index }} - {{ propiedad }} : {{ value }}
      </li>
    </ul>
  <br>
  <h2>Arreglo condicional - solucion incorrecta:</h2>
  <br>
    <ul>
      <li v-for="item in arrayFrutas" :key="item.name">
        <span v-if="item.stock > 0">
          {{ item.name }} - {{ item.price }}
        </span>
      </li>
    </ul>
    <br>
  <h2>Arreglo condicional - solucion correct:</h2>
  <br>
    <ul>
      <template v-for="item in arrayFrutas" :key="item.name">
        <li v-if="item.stock > 0">
          {{ item.name }} - {{ item.price }}
      </li>
      </template>
      
    </ul>
    <br>
    <button v-on:click.right.prevent="handleClick('Texto Right')">Activame Right</button>
    <button @click.left="handleClick('Texto Left')">Activame Left</button>
    <button @click.middle="handleClick('Texto Middle')">Activame middle</button>
    <br>
  </div>
    <br>
    <div class="container text-center mt-3">
      <h2>Renderizar</h2>
      <br>
      <h2 :class="classCounter">{{ counter }}</h2>
      <div class="btn-group">
        <button @click="increment" class="btn btn-success">Increment</button>
        <button @click="decrement" class="btn btn-danger">Decrement</button>
        <button @click="reset" class="btn btn-secondary">Reset</button>
        <button 
          @click="add" 
          :disabled="bloquearBtnAdd" 
          class="btn btn-primary">
          Add
        </button>
       
      </div>
        <ul class="list-group mt-4">
          <li
            class="list-group-item"
            v-for="(num, index) in arrayFavoritos" :key="index">
            {{ num }}
          </li>
        </ul>
  </div>
</template>
<style scoped>
h1 {
  color:red;
}
.positive {
  color:green;
}
.negative {
  color:red;
}
.zero {
  color : peru;
}
</style>