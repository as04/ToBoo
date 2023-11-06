<template>
    <v-card class="mx-auto" max-width="344">
      <v-btn
      class="edit-button"
      text
      color="teal accent-4"
      @click="isEditing = !isEditing"
    >
      {{ isEditing ? 'Save' : 'Edit' }}
    </v-btn>
    <v-card-text>
        <div class="scrollable-card">
        <div>Card {{ index + 1 }}</div>
        <!-- <p class="text-h4 text--primary">
            el·ee·mos·y·nar·y
        </p>
        <p>adjective</p>
        <div class="text--primary">
            relating to or dependent on charity; charitable.<br>
            "an eleemosynary educational institution."<br>
            more text <br>
            and more <br>
            moreeeeee!!!!!<br>
        </div> -->
        <div v-if="!isEditing">
          <p class="text-h4 text--primary">{{ title }}</p>
          <div class="text--primary">{{ description }}</div>
        </div>
        <div v-else>
          <v-text-field v-model="title" class="title-input" label="Title"></v-text-field>
          <v-textarea v-model="description" class="description-input" label="Description"></v-textarea>
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
        <CardDialog ref="cardDialog" />
        <v-btn
          text
          color="teal accent-4"
          @click="openDialog"
        >
          Expand
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
              Checklist
            </p>
            <!-- <p>This is the expanded content for Card {{ index + 1 }}.</p>
            <p>late 16th century (as a noun denoting a place where alms were distributed): from medieval Latin eleemosynarius, from late Latin eleemosyna ‘alms’, from Greek eleēmosunē ‘compassion’ </p> -->
            <!-- <h3>Checklist</h3> -->
            <div v-for="(item, index) in checklist" :key="index" style="display: flex; align-items: center;">
                <v-checkbox v-model="item.checked"></v-checkbox>
                {{ item.text }}
            </div>
            <!-- <v-checkbox label="Checkbox"></v-checkbox> -->
            <div class="input-container">
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
import CardDialog from './CardDialog.vue';
export default {
  data() {
    return {
      reveals: [],
      checklist: [],
      newItem: '',
      title: '',
      description: '',
      isEditing: false,
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
    openDialog() {
      this.$refs.cardDialog.openDialog({
      title: this.title,
      description: this.description,
      checklist: this.checklist,
    });
    },
  },
  components: {
    ProgressRing,
    CardDialog,
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
  props: {
    index: Number,
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

.input-container {
  margin-left: 20px; /* Adjust the margin to move the input to the right */
}

.edit-button {
  position: absolute;
  top: 10px; /* Adjust the top position as needed */
  right: 10px; /* Adjust the right position as needed */
}

</style>