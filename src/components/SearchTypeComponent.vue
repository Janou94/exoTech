<template>
  <div style="width: 200px">
    Type :
    <input
      type="text"
      v-model="value"
      v-on:click="searchType()"
      v-on:input='autoType()'
      v-on:focus="showAuto()"
    /><button v-on:click='delInput()'>&#128465;</button>
    <span> {{toSearch}} </span>
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
    searchType() {
      axios
        .get("https://api.magicthegathering.io/v1/types")
        .then((response) => {
          this.auto = JSON.parse(response.request.response).types;
        });
    },
    autoType() {
        axios
        .get("https://api.magicthegathering.io/v1/types")
        .then((response) => {
          this.auto = JSON.parse(response.request.response).types;
          this.auto = this.auto.filter(word => word.toLowerCase().includes(this.value.toLowerCase()));
        });
    },
    showAuto() {
      document.getElementById("autoType").style.visibility = "visible";
    },
    delInput() {
        this.toSearch='';
        this.$emit("searchType", this.toSearch);
        document.getElementById('autoType').style.visibility='hidden';
    },
    autoName(name) {
      this.toSearch += name + ",";
      this.$emit("searchType", this.toSearch);
    },
  },
  data() {
    return {
      value: "",
      auto: [],
      toSearch :'',
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