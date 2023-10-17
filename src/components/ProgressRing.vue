<template>
    <div class="progress-ring">
      <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40">
        <circle class="ring-background" cx="20" cy="20" r="15" />
        <circle
          class="ring"
          cx="20"
          cy="20"
          r="15"
          :stroke-dasharray="dashArray"
          :stroke-dashoffset="dashOffset"
        />
        <text class="progress-text" x="50%" y="50%" dy=".3em" text-anchor="middle">
          {{ progress }}%
        </text>
      </svg>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      progress: {
        type: Number,
        required: true,
      },
    },
    computed: {
      dashArray() {
        return 2 * Math.PI * 15;
      },
      dashOffset() {
        return this.dashArray * (1 - this.progress / 100);
      },
    },
  };
  </script>
  
  <style scoped>
  .progress-ring {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 40px;
  }
  
  .ring-background {
    fill: none;
    stroke: #ddd; /* Background color */
    stroke-width: 3;
  }
  
  .ring {
    fill: none;
    stroke: #2196F3; /* Progress color */
    stroke-width: 3;
  }
  
  .progress-text {
    font-size: 10px; /* Adjust the font size as needed */
    fill: #2196F3; /* Progress color */
  }
  </style>
  