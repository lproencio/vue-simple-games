<template>
  <div
    class="card_memory"
    :class="{ flip: clicked }"
    @click="flip_card(pokemon.id)"
  >
    <div class="card front" :class="pokemon.type[0]">
      <img :src="pokemon.img" />
      <p>{{ pokemon.name }}</p>
    </div>
    <div class="card back"><div></div></div>
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";
import { watch } from "@vue/runtime-core";
export default {
  name: "card_memory",
  props: {
    pokemon: Object,
    match_pokemon: Array,
    selected_pokemon: Array,
  },
  setup(props, { emit }) {
    const clicked = ref(false);

    watch(props, () => {
      if (
        !props.match_pokemon.includes(props.pokemon.id) &&
        props.selected_pokemon.length > 2
      ) {
        props.selected_pokemon.map((selected) => {
          if (selected == props.pokemon.id) {
            clicked.value = false;
          }
        });
      }
    });

    const flip_card = (id) => {
      clicked.value = !clicked.value;
      emit("selected_card", id);
    };
    return { clicked, flip_card };
  },
};
</script>
