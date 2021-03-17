<template>
  <div class="about">
    <div v-if="pokemon" class="w-3/12 m-auto bg-purple-100 mt-4 shadow-xl flex justify-center flex-col items-center">
      <h3 class="text-2xl text-green-900 uppercase">{{pokemon.name}}</h3>
      <div class="flex justify-center">
        <img class="w-48" :src="pokemon.sprites.front_default" alt="">
        <img class="w-48" :src="pokemon.sprites.back_default" alt="">
      </div>
      <h3 class="text-yellow-400"> Type</h3>
      <div v-for="(type, idx) in pokemon.types" :key="idx">
        <h5 class="text-blue-900">{{type.type.name}}</h5>
      </div>
      <h3 class="text-green-400"> Stats</h3>
      <div v-for="(stat, idx) in pokemon.stats" :key="idx">
        <h5 class="text-blue-900">{{stat.stat.name}}: {{stat.base_stat}}</h5>
      </div>
      <h3 class="text-green-400"> Hvilke moves kan {{pokemon.name}} lære?</h3>
      <div v-for="(move, idx) in pokemon.moves" :key="idx">
        <h5 class="text-blue-900">{{move.move.name}}: lvl {{move.version_group_details[0].level_learned_at}}, by: {{move.version_group_details[0].move_learn_method.name}}</h5>
      </div>
    </div>
  </div>
</template>
<script>
import {useRoute} from "vue-router";
import {reactive, toRefs} from "vue";

export default {
  

  setup() {
    const route = useRoute();

    const state = reactive({
      pokemon: null
    })

    fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
    .then((res)=> res.json())
    .then((data)=>{
      console.log(data);
      state.pokemon = data;
    })

    return{... toRefs(state)}
  }
}
</script>
