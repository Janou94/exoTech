<template>
  <div style="width: 200px">
    Rarity :
    <input
      type="text"
      v-model="value"
      v-on:input="searchRarity()"
      v-on:focus="showAuto()"
    /><button v-on:click='delInput()'>&#128465;</button>
    <span> {{toSearch}} </span>
    <ul class="autocomplete-results" id="autoRare">
      <li
        class="autocomplete-result"
        v-bind:key="rare.value"
        v-for="rare in raritiesArr"
        v-on:click="autoName(rare.value)"
      >
        {{ rare.value }}
      </li>
    </ul>
  </div>
</template>




<script>
export default {
  methods: {
    searchRarity() {
      this.raritiesArr=this.rarities.filter(rare => rare.value.toLowerCase().includes(this.value.toLowerCase()));
    },
    showAuto() {
      document.getElementById("autoRare").style.visibility = "visible";
    },
    delInput() {
        this.toSearch='';
        this.$emit("searchRarity", this.toSearch);
        document.getElementById('autoRare').style.visibility='hidden';
    },
    autoName(name) {
      this.toSearch = name;
      this.$emit("searchRarity", this.toSearch);
    },
  },
  created() {},
  data() {
    return {
      value: "",
      auto: [],
      raritiesArr: this.rarities,
      toSearch:''
    };
  },
  components: {},
  props: ["rarities"],
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