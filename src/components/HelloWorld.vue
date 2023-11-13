<template>
  <v-appp>
    <v-main>
      <div class="card-container">
        <div
          v-for="(card, index) in cards"
          :key="index"
          class="card"
        >
      <CardComponent :index="index"/>
        </div>
      </div>
    </v-main>
    <v-btn fab dark fixed bottom right color="primary" @click="addCard">
      <v-icon>mdi-plus</v-icon>
    </v-btn>
  </v-appp>
</template>

<script>
import CardComponent from './CardComponent.vue';
export default {
  data() {
    return {
      cards: [],
      cardCount: 0,
    };
  },
  methods: {
    addCard() {
      this.cardCount++;
      this.cards.push(this.cardCount);
    },
  },
  components: {
    CardComponent,
  },
};
</script>
<style>
.card-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
}

.card {
  margin: 10px;
}

</style>