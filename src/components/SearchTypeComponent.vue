<template>
  <div style="width: 200px">
    Type :
    <input
      type="text"
      v-model="value"
      v-on:click="searchName()"
      v-on:focus="showAuto()"
    />
    <ul class="autocomplete-results" id="autoType">
      <li
        class="autocomplete-result"
        v-bind:key="suggest.id"
        v-for="suggest in auto"
        v-on:click="autoName(suggest)"
      >
        {{ suggest }}
      </li>
    </ul>
  </div>
</template>




<script>
import axios from "axios";
export default {
  methods: {
    searchName() {
      //this.$emit('searchName', this.value)
      axios
        .get("https://api.magicthegathering.io/v1/types")
        .then((response) => {
          this.auto = JSON.parse(response.request.response).types;
        });
    },
    showAuto() {
      document.getElementById("autoType").style.visibility = "visible";
    },
    // hideAuto() {
    //     document.getElementById('autoName').style.visibility='hidden';
    // },
    autoName(name) {
      this.value += name + ",";
      this.$emit("searchType", this.value);
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