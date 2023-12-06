<template>
  <div id="app">
    <button @click="handleButtonClick" class="animated-button">
      Click me
    </button>
  </div>
</template>

<script>
export default {
  methods: {
    handleButtonClick() {
      // Your button click logic here
      console.log('Button clicked!');
    },
  },
};
</script>

<style>
.animated-button {
  /* Add your button styles here */
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.animated-button:active {
  /* Add your animation styles here */
  background-color: #3498db; /* Change to the color you want during the click animation */
  animation: clickAnimation 0.3s ease;
}

@keyframes clickAnimation {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}
</style>
