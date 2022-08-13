<template>
  <div style="width: 200px">
    Name : <input type="text" v-model="value" v-on:input="searchName()" />
  </div>
</template>




<script>
export default {
  methods: {
    searchName() {
      this.$emit("searchName", this.value);
    },
  },
  data() {
    return {
      value: "",
      auto: [],
    };
  },
  components: {},
};
</script>

<style scoped>
.autocomplete {
  position: relative;
}

.autocomplete-results {
  padding: 0;
  margin: 0;
  border: 1px solid #eeeeee;
  height: 120px;
  min-height: 1em;
  max-height: 6em;
  overflow: auto;
  visibility: hidden;
}

.autocomplete-result {
  list-style: none;
  text-align: left;
  padding: 4px 2px;
  cursor: pointer;
}

.autocomplete-result:hover {
  background-color: #4aae9b;
  color: white;
}
</style>