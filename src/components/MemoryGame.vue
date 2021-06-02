<template>
  <div class="memory_game">
    <h1>memory_game</h1>
    <card_memory />
  </div>
</template>

<script>
import card_memory from "@/components/card/Memory";

export default {
  name: "HelloWorld",

  components: {
    card_memory,
  },
};
</script>
