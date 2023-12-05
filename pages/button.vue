<template>
  <div class="center-container">
    <button
      ref="button"
      class="dummy-button"
      @click="handleButtonClick"
      @touchstart="handleButtonTouchStart"
      @touchend="handleButtonTouchEnd"
    >
      Draw
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {
    handleButtonTouchStart() {
      // Add styles for touch start if needed
      console.log("Touch start");
      this.$refs.button.classList.add("touch-active");
    },
    handleButtonTouchEnd() {
      // Add styles for touch end if needed
      console.log("Touch end");
      // Trigger the button click
      this.handleButtonClick();
      this.$refs.button.classList.remove("touch-active");
    },
  },
};
</script>

<style>
.dummy-button.touch-active {
  transition: transform 0.2s ease; /* Add a smooth transition effect */

  /* Your existing styles for the button */
}

.dummy-button.touch-active:active {
  transform: translateY(10px); /* Adjust the amount of movement as needed */
}
.center-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh; /* Set the height to 100% of the viewport height */
}

.dummy-button {
  position: relative;
  display: inline-block;
  margin: 20px;
}

.dummy-button {
  color: white;
  font-family: Helvetica, sans-serif;
  font-weight: bold;
  font-size: 36px;
  text-align: center;
  text-decoration: none;
  background-color: red;
  display: block;
  position: relative;
  padding: 50px 100px;

  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
  text-shadow: 0px 1px 0px #000;
  filter: dropshadow(color=#000, offx=0px, offy=1px);

  -webkit-box-shadow: inset 0 1px 0 #f9f6ee, 0 10px 0 #232b38;
  -moz-box-shadow: inset 0 1px 0 #f9f6ee, 0 10px 0 #232b38;
  box-shadow: inset 0 1px 0 #f9f6ee, 0 10px 0 #232b38;

  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
}

.dummy-button:active,
.dummy-button.touch-active {
  top: 10px;
  background-color: #2557af;

  -webkit-box-shadow: inset 0 1px 0 #f9f6ee, inset 0 -3px 0 #2558af6a;
  -moz-box-shadow: inset 0 1px 0 #f9f6ee, inset 0 -3pxpx 0 #2558af6a;
  box-shadow: inset 0 1px 0 #f9f6ee, inset 0 -3px 0 #2558af6a;
}

.dummy-button:after,
.dummy-button.touch-active:after {
  content: "";
  height: 100%;
  width: 100%;
  padding: 4px;
  position: absolute;
  bottom: -15px;
  left: -4px;
  z-index: -1;
  background-color: #2b1800;
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
}
</style>
