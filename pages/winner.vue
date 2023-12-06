<template>
  <v-card>
    <v-card-title>
      MLNG 45TH ANNIVERSARY | LIST OF LUCKY DRAW (5th December 2023)
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="items"
      :search="search"
      hide-default-footer
      disable-pagination
      loading="true"
      dense
    ></v-data-table>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      headers: [
        { text: "Name", value: "name" },
        { text: "Number", value: "number" },
        { text: "Prize", value: "prize" },
      ],
      items: [],
      search: "",
    };
  },

  async mounted() {
    await this.fetchWinner();
  },

  methods: {
    async fetchWinner() {
      try {
        const response = await this.$axios.get("/winners");
        this.items = response.data;
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    },
  },
};
</script>

<style>
/* Add your custom styles here */
</style>
