<template>
  <div>
    <div class="content">
      <div class="wraper">
        <div class="wraper-input">
          <SelectedItem
            class="selected"
            v-for="country in selectedCountries"
            :key="country.name"
            :name="country.name"
          />
          <input
            v-model="search"
            type="text"
            placeholder="Input country here"
            class="input"
          />
        </div>
        <Dropdown
          class="dropdown"
          @select-item="setSelectedCountry"
          v-if="isOpen"
          v-bind:countries="result"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SelectedItem from "./SelectedItem.vue";
import Dropdown from "./Dropdown.vue";

export default {
  name: "AutoMulti",
  components: {
    SelectedItem,
    Dropdown,
  },

  props: {
    data: {
      type: Array,
    },
  },

  data() {
    return {
      selectedCountries: ([] = []),
      isOpen: false,
      search: "",
      noResult: "Not Found",
      result: ([] = []),
    };
  },

  methods: {
    setResult() {
      this.search = "";
      this.isOpen = false;
      this.noResult = "Not Found";
    },
    filterResults() {
      this.result = this.data.filter((item) => {
        return item.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1;
      });
    },
    setSelectedCountry(country) {
      this.selectedCountries.push(country);
      this.search = "";
    },
  },

  mounted() {
    console.log(this.data, "mounted");
  },

  watch: {
    countries: function (value, oldValue) {
      console.log(value, "oldValue");
    },
    search: function (value, oldValue) {
      if (value === "") {
        this.isOpen = false;
      } else {
        this.filterResults();
        this.isOpen = true;
      }
    },
  },
};
</script>

<style scoped>
* {
  margin: 0px;
  padding: 0px;
}

p {
  margin: 0px;
  padding: 0px;
}

.content {
  width: 50%;
}

.input {
  /* background-color: #ee82ee; */
  min-width: 5rem;
  max-width: 10rem;
  border: none;
  margin-left: 0.5rem;
  min-height: 30px;
}

.input {
  border: none;
}

.selected {
  margin: 2px 2px 2px 2px;
}

.input:focus {
  outline: none;
}

.wraper-input {
  /* background-color: blue; */
  width: 35rem;
  min-height: 30px;
  max-height: auto;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  flex-flow: row wrap;
  border: 3px solid #003d61;
  border-radius: 7px;
}

.wraper {
  /* background-color: orange; */
  display: row;
  width: 100%;
}

.dropdown {
  position: absolute;
  z-index: 9999;
  margin: 5px 0px 0px 0px;
  width: 35rem;
  border-radius: 5px;
}
</style>
