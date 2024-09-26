<template>
<!-- Her er vores dom elementer -->

<!--indsat billede fra nettet-->
<img
  src="https://chirpforbirds.com/wp-content/uploads/2021/02/Blog-featured-image-2-Kingfisher.jpg"
  alt="Kingfisher"
  width="400"
/>

<h1>Pepita's energy: {{ pepita.energy }}</h1>

<input type="number" v-model="gramsToEat" placeholder="Grams" />
<button @click="eat">Eat</button>

<input type="number" v-model="kmsToFly" placeholder="Kilometers" />
<button @click="fly">Fly</button>
</template>

<script>
import { ref, reactive } from 'vue'; 

export default { 
setup() { 
  // Mine variabler
  const gramsToEat = ref(0);
  const kmsToFly = ref(0);

  //mine objekter
  const pepita = reactive({
    energy: 0,
  });

  // mine funktioner
  function eat() {
    pepita.energy += gramsToEat.value * 4;
  }

  function fly() {
    pepita.energy -= kmsToFly.value * 2 + 10;
  }

  // Husk at return'e alt!!
  return {
    gramsToEat,
    kmsToFly,
    eat,
    pepita,
    fly,
  };
}
};
</script>