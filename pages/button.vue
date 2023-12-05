<template>
  <div class="center-container">
    <!-- <v-btn
      class="ma-2"
      :loading="loading4"
      :disabled="loading4"
      color="info"
      @click="loader = 'loading4'"
      x-large
      style="height: 80px; min-width: 134px"
    >
      PLAY
      <template v-slot:loader>
        <span class="custom-loader">
          <v-icon light>mdi-cached</v-icon>
        </span>
      </template>
    </v-btn> -->
    <button class="dummy-button">Draw</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loader: null,
      loading: false,
      loading2: false,
      loading3: false,
      loading4: false,
      loading5: false,
    };
  },
  methods: {
    // buttonClick() {
    //   alert('Button clicked!');
    // },
  },
  watch: {
    loader() {
      const l = this.loader;
      this[l] = !this[l];

      setTimeout(() => (this[l] = false), 3000);

      this.loader = null;
    },
  },
};
</script>

<style>
.center-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh; /* Set the height to 100% of the viewport height */
}

.styled-button {
  font-size: 24px; /* Set the font size */
  padding: 20px 40px; /* Set padding to make the button larger */
  background-color: #4caf50; /* Set the background color */
  color: #ffffff; /* Set the text color */
  border-radius: 10px; /* Add border-radius for rounded corners */
  cursor: pointer; /* Add pointer cursor on hover */
  transition: background-color 0.3s ease; /* Add a smooth transition for background color */
}

.styled-button:hover {
  background-color: #45a049; /* Change background color on hover */
}

  .dummy-button{
    position:relative;
    display:inline-block;
    margin:20px;
  }
  
  .dummy-button{
    color:white;
    font-family:Helvetica, sans-serif;
    font-weight:bold;
    font-size:36px;
    text-align: center;
    text-decoration:none;
    background-color: red;
    display:block;
    position:relative;
    padding: 50px 100px;
    
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
    text-shadow: 0px 1px 0px #000;
    filter: dropshadow(color=#000, offx=0px, offy=1px);
    
    -webkit-box-shadow:inset 0 1px 0 #F9F6EE, 0 10px 0 #232b38;
    -moz-box-shadow:inset 0 1px 0 #F9F6EE, 0 10px 0 #232b38;
    box-shadow:inset 0 1px 0 #F9F6EE, 0 10px 0 #232b38;
    
    -webkit-border-radius: 5px;
    -moz-border-radius: 5px;
    border-radius: 5px;
  }
  
  .dummy-button:active{
    top:10px;
    background-color:#2557AF;
    
    -webkit-box-shadow:inset 0 1px 0 #F9F6EE, inset 0 -3px 0 #2558af6a;
    -moz-box-shadow:inset 0 1px 0 #F9F6EE, inset 0 -3pxpx 0 #2558af6a;
    box-shadow:inset 0 1px 0 #F9F6EE, inset 0 -3px 0 #2558af6a;
  }
  
  .dummy-button:after{
    content:"";
    height:100%;
    width:100%;
    padding:4px;
    position: absolute;
    bottom:-15px;
    left:-4px;
    z-index:-1;
    background-color:#2B1800;
    -webkit-border-radius: 5px;
    -moz-border-radius: 5px;
    border-radius: 5px;
  }

/* .custom-loader {
  animation: loader 1s infinite;
  display: flex;
}
@-moz-keyframes loader {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
@-webkit-keyframes loader {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
@-o-keyframes loader {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
@keyframes loader {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
} */
</style>
