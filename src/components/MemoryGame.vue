<template>
  <div class="memory_game">
    <h1>memory_game</h1>
    <div class="all_cards">
      <div class="item_list" v-for="(pokemon, i) in all_pokemon" :key="i">
        <CardMemory :pokemon="pokemon" @selected_card="selected_card" />
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";

import CardMemory from "@/components/card/Memory";
import pokemons from "@/jsons/pokemons.json";

export default {
  name: "HelloWorld",
  components: {
    CardMemory,
  },
  setup() {
    const all_pokemon = ref([]);

    const shuffle = (array) => {
      var currentIndex = array.length,
        randomIndex;

      while (0 !== currentIndex) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex--;

        [array[currentIndex], array[randomIndex]] = [
          array[randomIndex],
          array[currentIndex],
        ];
      }

      return array;
    };

    all_pokemon.value = shuffle(pokemons.pokemon);

    const selected_card = (id) => {
      console.log(id);
    };

    return { all_pokemon, selected_card };
  },
};
</script>
