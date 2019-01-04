<template>
  <div class="cards">
    <GameCard
      v-for="(card, index) in cards"
      :key="card"
      :card="card"
      :is-current="index === 0"
      @cardKnown="$emit('cardKnown');"
      @cardUnknown="$emit('cardUnknown');"
    />
    <h2 style="color:black; top:300px;">{{ pile }}</h2>
  </div>
</template>

<script>
import GameCard from "@/components/GameCard";

export default {
  components: {
    GameCard
  },

  props: {
    cards: {
      type: Array,
      required: true
    },
    pile: {
      type: String,
      required: true
    }
  }
};
</script>

<style lang="scss" scoped>
.cards {
  position: relative;
  display: inline-block;
  margin: 50px;
  width: 150px;
}
</style>
