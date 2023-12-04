<template>
  <div>
    <div style="height: 10vh">
      <h1>MLNG Best Dress Award (Women)</h1>
    </div>
    <div style="display: flex; justify-content: space-evenly; height: 50vh">
      <div v-for="dress in dresses" :key="dress.id">
        <img
          :src="dress.imageUrl"
          alt="Dress Image"
          style="max-width: 200px; margin-bottom: 10px"
        />
        <h3>{{ dress.name }}</h3>
        <h5>{{ dress.wearer }}</h5>
        <p>Votes: {{ dress.votes }}</p>
      </div>
    </div>
    <div>
      <div ref="chart" style="height: 40vh"></div>
    </div>
  </div>
</template>

<script>
import * as echarts from "echarts";
import io from "socket.io-client";

export default {
  data() {
    return {
      dresses: [],
    };
  },

  async mounted() {
    await this.fetchDresses();
    // Establish WebSocket connection
    const socket = io(
      process.env.NODE_ENV === "production"
        ? "https://mlng-best-dress-backend.onrender.com"
        : "http://localhost:3030"
    );

    // Listen for real-time updates
    socket.on("updateVotes", (data) => {
      // Handle the real-time update, e.g., update the local state
      console.log("Real-time update received:", data);
      let dress = data.filter((e) => e.gender === "female");
      this.dresses = dress;
    });

    this.$nextTick(() => {
      this.renderChart();
    });

    // Listen for the "F" key press to toggle fullscreen
    document.addEventListener("keydown", (event) => {
      if (event.key === "F" || event.key === "f") {
        this.toggleFullscreen();
      }
    });
  },

  watch: {
    dresses: {
      handler: "renderChart",
      deep: true,
    },
  },

  methods: {
    async fetchDresses() {
      try {
        const response = await this.$axios.get("/dresses");
        let dress = response.data.filter((e) => e.gender === "female");
        this.dresses = dress;
      } catch (error) {
        console.error("Error fetching dresses:", error);
      }
    },

    async voteForDress(dressId) {
      try {
        await this.$axios.post(`/dresses/${dressId}/vote`);
        await this.fetchDresses(); // Refresh the dress list after voting
      } catch (error) {
        console.error("Error voting for dress:", error);
      }
    },

    renderChart() {
      const chartData = this.dresses.map((dress) => ({
        name: dress.name,
        value: dress.votes,
      }));

      const chart = echarts.init(this.$refs.chart);
      chart.setOption({
        title: {
          // text: "Voting Results",
          // subtext: "Number of Votes for Each Dress",
          x: "center",
        },
        // tooltip: {
        //   trigger: "item",
        //   formatter: "{a} <br/>{b} : {c} ({d}%)",
        // },
        xAxis: {
          type: "category",
          data: this.dresses.map((dress) => dress.name),
        },
        yAxis: {
          type: "value",
        },
        series: [
          {
            name: "Votes",
            type: "bar",
            data: chartData,
            label: {
              show: true,
              position: "top", // You can adjust the position as needed
              formatter: "{c}", // Display the value of the bar
            },
          },
        ],
      });
    },

    toggleFullscreen() {
      this.fullscreen = !this.fullscreen;

      // Use the Fullscreen API to toggle fullscreen mode
      if (this.fullscreen) {
        document.documentElement.requestFullscreen();
      } else {
        document.exitFullscreen();
      }
    },
  },
};
</script>

<style>
html,
body {
  height: 100%;
  margin: 0;
  padding: 0;
}
</style>
