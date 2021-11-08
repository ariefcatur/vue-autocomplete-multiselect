<template>
  <div v-if="isClicked" class="container">
    <button @click="close" class="close">x</button>
    <div class="title-wraper">
      <p class="title">{{ name }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isClicked: true,
    };
  },

  methods: {
    close() {
      this.isClicked = false;
    },
  },

  props: {
    name: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped>
.container {
  background-color: #003d61;
  display: flex;
  flex-direction: row;
  flex-wrap: row;
  width: auto;
  height: 1.5rem;
  text-align: center;
  padding: 3px 5px 3px 5px;
  border-radius: 3px;
}

p {
  margin: 0px;
  padding: 0px;
  width:auto;
  color: white;
}

.title-wraper {
  height: inherit;
  width: auto;
  
}

.title {
  height: inherit;
  text-align: center;
  align-items: center;
}

.close {
  margin: 0px 2px 0px 0px;
  background-color: transparent;
  border: none;
  color: white;
  font-size: 12px;
  font-weight: 600;
}
</style>