<template>
  <div class="card_memory" :class="{ flip: clicked }" @click="flip_card">
    <div class="card front">Front</div>
    <div class="card back"><div></div></div>
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";
export default {
  name: "card_memory",
  setup() {
    const clicked = ref(false);

    const flip_card = () => {
      clicked.value = !clicked.value;
    };
    return { clicked, flip_card };
  },
};
</script>
