<template>
<div style='width:200px'>
    Rarity : <input type='text'  v-model='value' v-on:input="searchRarity()" v-on:focus="showAuto()">
    <ul class="autocomplete-results" id='autoRare'>
      <li class="autocomplete-result" v-bind:key='rare.value' v-for='rare in raritiesArr' v-on:click="autoName(rare.value)">
            {{rare.value}}
      </li>
    </ul>
</div>
</template>




<script>
        export default  {
            methods: {
                searchRarity() {
                    this.$emit('searchRarity', this.value)
                },
                showAuto() {
                    document.getElementById('autoRare').style.visibility='visible';
                },
                // hideAuto() {
                //     document.getElementById('autoName').style.visibility='hidden';
                // },
                autoName(name) {
                    this.value=name
                    this.$emit('searchRarity', this.value)
                }

            },
            created() {
            },
            data() {
                return {
                    value:'',
                    auto:[],
                    raritiesArr: this.rarities
                }
            },
            components: {
                
            },
            props: ['rarities'],
        }
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
    background-color: #4AAE9B;
    color: white;
  }
</style>