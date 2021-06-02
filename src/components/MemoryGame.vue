<template>
  <div class="memory_game">
    <h1>memory_game</h1>
    <CardMemory />
  </div>
</template>

<script>
import CardMemory from "@/components/card/Memory";

export default {
  name: "HelloWorld",

  components: {
    CardMemory,
  },
};
</script>
