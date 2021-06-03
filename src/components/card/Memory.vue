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
export default {
  name: "card_memory",
  props: { pokemon: Object },
  setup(_, { emit }) {
    const clicked = ref(false);

    const flip_card = (id) => {
      clicked.value = !clicked.value;
      emit("selected_card", id);
    };
    return { clicked, flip_card };
  },
};
</script>
