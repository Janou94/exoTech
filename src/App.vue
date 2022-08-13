<template>
  <div id="app">
    <div class='inputContainer'>
      <span><SearchNameComponent @searchName='searchName'></SearchNameComponent></span>
      <span><SearchTypeComponent @searchRarity='searchType'></SearchTypeComponent></span>
      <span><SearchRarityComponent @searchRarity='searchRarity' v-bind:rarities='this.rarities'></SearchRarityComponent></span>
    </div>
    <div class='flex'>
      <div class='cardBlock' v-bind:key='card.id' v-for='card in cards' :style="{ 'background-color': rarities[rarities.findIndex(
                    element => element.value === card.rarity)].color }">
          <h1 class='cardTitle'> {{card.name}} </h1>
          <span> {{card.text}} </span>
          <span> {{card.type}} </span>
          <span> {{card.rarity}} </span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import SearchNameComponent from './components/SearchNameComponent.vue'
import SearchRarityComponent from './components/SearchRarityComponent.vue'

const rarities = [
  { value: 'Common', color: '#2e2e2e' },
  { value: 'Uncommon', color: '#ababab' },
  { value: 'Rare', color: '#ffca00' },
  { value: 'Mythic Rare', color: '#ff8600' },
  { value: 'Special', color: '#fd6ee1' },
  { value: 'Basic Land', color: '#000000' },
];

export default {
  data() {
    return {
      cards:[],
      rarities:[]
    }
  },
  created() {
    axios
      .get('https://api.magicthegathering.io/v1/cards?pageSize=30')
      .then((response) => {
        this.cards = JSON.parse(response.request.response).cards
      }),
      this.rarities=rarities;
  },
  name: 'App',
  components : {
    SearchNameComponent,
    SearchRarityComponent
  },
  methods: {
    searchName(value) {
      axios
      .get('https://api.magicthegathering.io/v1/cards?pageSize=30&name='+value)
      .then((response) => {
        this.cards = JSON.parse(response.request.response).cards
      })
      this.rarities=rarities;
    },
    searchRarity(value) {
      axios
      .get('https://api.magicthegathering.io/v1/cards?pageSize=30&rarity='+value)
      .then((response) => {
        this.cards = JSON.parse(response.request.response).cards
      })
      this.rarities=rarities;
    }
  }

}


</script>

<style>
.inputContainer {
  margin-bottom:200px;
  display: flex;
  flex-direction: revert;
  justify-content: space-around;
}
a {
  color:#fafafa;
  text-decoration: none;
  font-weight:bolder;
  padding:5px;
}

button, input[type="submit"], input[type="reset"] {
	background: none;
	color: inherit;
	border: none;
	padding: 0;
	font: inherit;
	cursor: pointer;
	outline: inherit;
}
input[type="text"] {
	background: none;
	color: inherit;
	border: none;
	padding: 0;
	outline: inherit;
  background-color:#fafafa;
  border-radius:5px;
  height:50px;
  width:200px;
  color:black;
  margin-top:10px;
}
span {
  font-size:20px;
  font-weight: bold;
}

html {
  background-color:black;
  color: #fafafa;
  height:100%
}
body {
  height:100%
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color:black;
  color: #fafafa;
  height:100%;
}
.flex {
  display:flex;
  justify-content: space-around;
  width:100%;
  flex-wrap:wrap;
  gap:50px
}
.flex2 {
  display:flex;
  flex-direction: column;
  justify-content: space-between;
  width:100%
}

.cardBlock {
  display: flex;
  flex-direction: column;
  height:800px;
  width:400px;
  position:relative;
  border-radius:20px;
  justify-content:space-between
}

.cardTitle {

}

</style>
