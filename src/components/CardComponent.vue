<template>
    <v-card class="mx-auto" max-width="344">
    <v-card-text>
        <div class="scrollable-card">
        <div>Card {{ index + 1 }}</div>
        <p class="text-h4 text--primary">
            el·ee·mos·y·nar·y
        </p>
        <p>adjective</p>
        <div class="text--primary">
            relating to or dependent on charity; charitable.<br>
            "an eleemosynary educational institution."<br>
            more text <br>
            and more <br>
            moreeeeee!!!!!<br>
        </div>
        </div>
    </v-card-text>

    <v-card-actions>
        <div class="button-and-progress-container">
        <v-btn
        text
        color="teal accent-4"
        @click="toggleReveal(index)"
        >
        {{ reveals[index] ? 'Close' : 'Learn More' }}
        </v-btn>
        <ProgressRing :progress="calcProgress" />
    </div>
    </v-card-actions>

    <v-expand-transition>
        <v-card
        v-if="reveals[index]"
        class="transition-fast-in-fast-out v-card--reveal"
        style="height: 100%;"
        >
        <v-card-text class="pb-0">
            <div class="scrollable-card">
            <p class="text-h4 text--primary">
                Origin
            </p>
            <!-- <p>This is the expanded content for Card {{ index + 1 }}.</p>
            <p>late 16th century (as a noun denoting a place where alms were distributed): from medieval Latin eleemosynarius, from late Latin eleemosyna ‘alms’, from Greek eleēmosunē ‘compassion’ </p> -->
            <h3>Checklist</h3>
            <div v-for="(item, index) in checklist" :key="index" style="display: flex; align-items: center;">
                <v-checkbox v-model="item.checked"></v-checkbox>
                {{ item.text }}
            </div>
            <!-- <v-checkbox label="Checkbox"></v-checkbox> -->
            <div>
            <input v-model="newItem" @keydown.enter="addItem" placeholder="Add a new item">
            </div>
            </div>
        </v-card-text>
        <v-card-actions class="pt-0">
            <v-btn
            text
            color="teal accent-4"
            @click="toggleReveal(index)"
            >
            Close
            </v-btn>
        </v-card-actions>
        </v-card>
    </v-expand-transition>
    </v-card>
</template>

<script>
import ProgressRing from './ProgressRing.vue';
export default {
  data() {
    return {
      cards: [],
      cardCount: 0,
      reveals: [],
      // progressValue: 90,
      checklist: [],
      newItem: '',
    };
  },
  methods: {
    toggleReveal(index) {
      this.$set(this.reveals, index, !this.reveals[index]);
    },
    addItem() {
      if (this.newItem.trim() !== '') {
        this.checklist.push({ text: this.newItem, checked: false });
        this.newItem = '';
      }
    },
  },
  components: {
    ProgressRing,
  },
  computed: {
    calcProgress() {
      const completedItems = this.checklist.filter((item) => item.checked).length;
      const totalItems = this.checklist.length;
      const progress = totalItems > 0 ? (completedItems / totalItems) * 100 : 0;
      if (Number.isInteger(progress)) {
      return progress.toFixed(0); // No decimal places for whole numbers
      } 
      else {
      return progress.toFixed(1); // Display one decimal place for values with a decimal part
     }
    },
  },
};
</script>
<style>
.v-card--reveal {
  bottom: 0;
  opacity: 1 !important;
  position: absolute;
  width: 100%;
}
.card-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
}

.card {
  margin: 10px;
}

.scrollable-card {
  max-height: 200px; /* Adjust the max height as needed */
  overflow-y: auto;
}

.button-and-progress-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

</style>