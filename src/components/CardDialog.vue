<template>
    <v-dialog v-model="dialogVisible">
      <v-card>
        <v-card-title>{{ card.title }}</v-card-title>
        <v-card-text>
          <!-- Display the card's description, checklist, or other content here -->
          <p>{{ card.description }}</p>
          <ul>
            <li v-for="item in card.checklist">{{ item.text }}</li>
          </ul>
        </v-card-text>
        <v-card-actions>
          <v-btn @click="closeDialog">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </template>
  
  <script>
  export default {
    props: {
      card: Object, // Pass the card data as a prop
    },
    data() {
      return {
        dialogVisible: false,
      };
    },
    methods: {
      openDialog() {
        this.dialogVisible = true;
      },
      closeDialog() {
        this.dialogVisible = false;
      },
    },
  };
  </script>
  