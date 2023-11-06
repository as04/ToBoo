   <template>
    <v-dialog v-model="dialog" max-width="50%">
      <v-card>
        <v-card-title>
          <!-- Card content here -->
          {{ cardData.title }}
        </v-card-title>
        <v-card-text>
          <!-- Card content here -->
          {{ cardData.description }}
        </v-card-text>
        <v-card-actions>
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
      cardData: {
        title: "",
        description: "",
        checklist: [],
      },
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
    },
  };
  </script>
  