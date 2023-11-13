   <template>
    <v-dialog v-model="dialog" max-width="50%">
      <v-card>
        <v-card-title>
          <!-- Card content here -->
          <v-text-field v-model="title" class="title-input" label="Title"></v-text-field>
        </v-card-title>
        <v-card-text>
          <!-- Card content here -->
          <v-textarea v-model="description" class="description-input" label="Description"></v-textarea>
          <div v-for="(item, index) in checklist" :key="index" style="display: flex; align-items: center;">
                <v-checkbox v-model="item.checked"></v-checkbox>
                {{ item.text }}
            </div>
            <!-- <v-checkbox label="Checkbox"></v-checkbox> -->
            <div class="input-container">
              <input v-model="newItem" @keydown.enter="addItem" placeholder="Add a new item">
            </div>
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" @click="saveChanges">Save</v-btn>
          <v-btn color="primary" @click="closeDialog">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </template>
  
  <script>
  export default {
    // props: {
    //   cardData: Object, // Pass card data to the dialog
    // },
    data() {
      return {
        dialog: false,
    //   cardData: {
        title: "",
        description: "",
        checklist: [],
        newItem: '',
    //   },
      };
    },
    methods: {
      openDialog(data) {
        this.dialog = true;
        this.cardData = data;
      },
      closeDialog() {
        this.dialog = false;
      },
      saveChanges() {
        // Emit an event to the parent component with updated title and description
        this.$emit('save-card', {
            title: this.title,
            description: this.description,
            checklist: this.checklist,
        });
        this.dialog = false; // Close the dialog
        },
        addItem() {
      if (this.newItem.trim() !== '') {
        this.checklist.push({ text: this.newItem, checked: false });
        this.newItem = '';
      }
    },
    },
    props: {
    index: Number,
  },
  };
  </script>
  