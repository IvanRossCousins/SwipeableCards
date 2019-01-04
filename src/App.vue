<template>
  <div id="app">
    <div>
      <GameCardsStackIN :cards="unknownCards" :pile="unknown" />
      <GameCardsStack
        :cards="visibleCards"
        @cardKnown="handleCardKnown"
        @cardUnknown="handleCardUnknown"
        :pile="vis"
      />
      <GameCardsStackIN :cards="dislikedCards" :pile="disliked" />
      <GameCardsStack
        :cards="knownCards"
        @cardKnown="handleCardLiked"
        @cardUnknown="handleCardDisliked"
        :pile="known"
      />
      <GameCardsStackIN :cards="likedCards" :pile="liked" />
    </div>
    <div><button v-on:click="finish">Finish</button></div>
  </div>
</template>

<script>
import GameCardsStack from "./components/GameCardsStack";
import GameCardsStackIN from "./components/GameCardsStackIN";

var fs = require("fs");
var text = fs.readFileSync("./text.txt");
var originalcardtext = text.toString().split("\n");
var cardtext = originalcardtext;
var unknownList = [];
var likedList = [];
var dislikedList = [];

export default {
  name: "App",
  components: {
    GameCardsStack,
    GameCardsStackIN
  },

  data() {
    return {
      visibleCards: cardtext,
      knownCards: [],
      unknownCards: [],
      likedCards: [],
      dislikedCards: [],
      vis: "Unsorted",
      known: "Known",
      unknown: "Unknown",
      liked: "Liked",
      disliked: "Disliked"
    };
  },

  methods: {
    handleCardKnown() {
      console.log("handleCardKnown");
      this.knownCards.push(this.visibleCards.shift());
      console.log(this.knownCards);
    },
    handleCardUnknown() {
      console.log("handleCardUnknown");
      this.unknownCards.push(this.visibleCards.shift());
      console.log(this.unknownCards);
    },
    handleCardLiked() {
      console.log("handleCardLiked");
      this.likedCards.push(this.knownCards.shift());
      console.log(this.likedCards);
    },
    handleCardDisliked() {
      console.log("handleCardDisliked");
      this.dislikedCards.push(this.knownCards.shift());
      console.log(this.dislikedCards);
    },
    finish() {
      unknownList = this.unknownCards;
      likedList = this.likedCards;
      dislikedList = this.dislikedCards;
    }
  }
};
</script>

<style lang="scss">
@import "./styles/mixins.scss";

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  text-align: center;
}
</style>
