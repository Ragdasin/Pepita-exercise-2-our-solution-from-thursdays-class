<template>
  <!-- Her er vores dom elementer -->

  <!--indsat billede fra nettet-->
  <img src="https://chirpforbirds.com/wp-content/uploads/2021/02/Blog-featured-image-2-Kingfisher.jpg" alt="Kingfisher"
    width="400" />
  <!--Our display for pepitas values-->
  <h2>Pepita's energy: {{ pepita.energy }}</h2>
  <h2>Pepita's location: {{ pepita.location }}</h2>
  <h2>Visited cities: {{ pepita.visitedCities }}</h2>

  <!--our fly/eat buttons-->
  <input type="number" v-model="gramsToEat" placeholder="Grams" />
  <button @click="eat">Eat</button>

  <input type="number" v-model="kmsToFly" placeholder="Kilometers" />
  <button @click="fly">Fly</button>

  <!--list rending of all our cities-->
  <div v-for="city in cityInfo.cityNames">
    <button @click="goToPlace(city)">{{ city }}</button>
  </div>
</template>

<script>
import { ref, reactive } from 'vue';

export default {
  setup() {
    // My reactive variables
    const gramsToEat = ref(0);
    const kmsToFly = ref(0);

    //My objects
    const pepita = reactive({
      energy: 0,
      location: 'Aarhus',
      visitedCities: ['Aarhus']
    });

    const cityInfo = reactive({
      cityNames: ['Aarhus', 'Copenhagen', 'Nuuk', 'New York', 'The Moon', 'Atlantis'],
      cityLocation: [0, 300, 4500, 7500, 250000, 3000]
    });




    // My functions
    function eat() {
      pepita.energy += gramsToEat.value * 4;
    }

    function fly() {
      pepita.energy -= kmsToFly.value * 2 + 10;
    }

    function goToPlace(placeToGo) {
      //calculating the distance
      let cityFromIndex = cityInfo.cityNames.indexOf(pepita.location)
      let cityToIndex = cityInfo.cityNames.indexOf(placeToGo)
      let cityToLocation = cityInfo.cityLocation[cityToIndex]
      let cityFromLocation = cityInfo.cityLocation[cityFromIndex]
      let distance = Math.abs(cityFromLocation - cityToLocation)
      //only execute if pepita is not already there!
      if (pepita.location != placeToGo){
      //only execute if pepita has enough energy
      if (pepita.energy >= distance * 2 + 10) {
        pepita.energy -= distance * 2 + 10;
        pepita.location = placeToGo

        //avoid dublicates
        if (!pepita.visitedCities.includes(placeToGo))
          pepita.visitedCities.push(placeToGo)
      } else {
        alert(`pepita can't travel ${distance} km to ${placeToGo} - eat more seeds`)
      }
    } else {
      alert(`You are already in ${placeToGo}`)
    }
    }

    // Remember to return!
    return {
      gramsToEat,
      kmsToFly,
      eat,
      pepita,
      fly,
      goToPlace,
      cityInfo,



    };
  }
};
</script>