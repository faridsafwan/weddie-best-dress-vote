<template>
  <v-container>
    <v-row justify="center">
      <v-col v-for="dress in dresses" :key="dress.id" cols="12" sm="6" md="4">
        <v-card>
          <v-img
            :src="dress.imageUrl"
            alt="Dress Image"
            class="mx-auto"
          ></v-img>
          <v-card-title>{{ dress.name }}</v-card-title>
          <v-card-text>{{ dress.wearer }}</v-card-text>
          <!-- Card Action Button -->
          <v-card-actions class="text-center">
            <v-spacer></v-spacer>
            <v-btn x-large @click="voteForDress(dress.id)" color="primary">
              Vote !
            </v-btn>
            <v-spacer></v-spacer>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  data() {
    return {
      dresses: [],
    };
  },

  async mounted() {
    await this.fetchDresses();
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
  },
};
</script>

<style scoped>
/* You can add custom styles here if needed */
.mx-auto {
  margin-left: auto;
  margin-right: auto;
}
</style>
