<template>
  <div id="app" class="form">
    <AutoMulti v-bind:data="countries"/>
  </div>
</template>

<script>
import AutoMulti from "./components/AutoMulti.vue";

export default {
  name: "App",
  components: {
    AutoMulti,
  },

  data() {
    return {
      countries: ([] = [])
    };
  },

  created() {
    var that = this;
    fetch("https://api.first.org/data/v1/countries?q=in")
      .then((response) => response.json())
      .then((data) => {
        var object = data.data;
        let count = [];
        for (const property in object) {
          count.push({ name: object[property].country });
          console.log(`${property}: ${object[property]}`);
        }
        console.log(count, "count");
        that.countries = count;
      });
  },

  
};
</script>

<style scoped>
* {
  margin: 0px;
  padding: 0px;
}


</style>
