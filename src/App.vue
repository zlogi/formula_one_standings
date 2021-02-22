<template>
  <div class="table">
    <drivers-table v-bind:standingsDriver="standingsDriver"></drivers-table>

  </div>
</template>

<script>
import Table from "@/components/DriversTable.vue";

export default {
  name: "App",
  components: {
    "drivers-table": Table,
  },
  data() {
    return {
      standingsDriver: [],
    };
  },

  mounted: async function() {
    const axios = require("axios");
    const response = await axios
      .get("http://ergast.com/api/f1/2019/5/driverStandings.json");
      this.standingsDriver =
          response.data.MRData.StandingsTable.StandingsLists[0].DriverStandings;

    // axios
    //   .get("http://ergast.com/api/f1/2019/5/driverStandings.json")
    //   .then((response) => {
    //     this.standingsDriver =
    //       response.data.MRData.StandingsTable.StandingsLists[0].DriverStandings;
    //     console.log(response.data);
    //   })
    //   .catch((error) => {
    //     console.log(error);
    //   });
  },
};
</script>

<style scoped></style>
