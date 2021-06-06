<template>
  <div class="memory_game">
    <h1>memory_game</h1>
    <div class="all_cards">
      <div class="item_list" v-for="(pokemon, i) in all_pokemon" :key="i">
        <CardMemory
          :pokemon="pokemon"
          @selected_card="selected_card"
          :match_pokemon="match_pokemon"
          :selected_pokemon="selected_pokemon"
        />
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
    const selected_pokemon = ref([]);
    const match_pokemon = ref([]);

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

    const valid_match = (id) => {
      console.log(selected_pokemon.value.includes(id));
      if (selected_pokemon.value.includes(id)) {
        match_pokemon.push(selected_pokemon.value[0]);
        return;
      }

      selected_pokemon.value.push(0);

      console.log(selected_pokemon.value);

      setTimeout(() => {
        selected_pokemon.value = [];
      }, 2000);

      console.log(selected_pokemon.value);
    };

    const selected_card = (id) => {
      switch (selected_pokemon.value.length) {
        case 0:
          selected_pokemon.value.push(id);
          break;

        case 1:
          valid_match(id);
          break;

        default:
          selected_pokemon.value = [];
          break;
      }
    };

    return {
      all_pokemon,
      selected_card,
      match_pokemon,
      selected_pokemon,
    };
  },
};
</script>
