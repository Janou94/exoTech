<template>
<div style='width:200px'>
    <input type='text'  v-model='value' v-on:input="searchName()" v-on:focus="showAuto()">
    <div class="autocomplete-results" id='autoName'>
      <span class="autocomplete-result" v-bind:key='suggest.id' v-for='suggest in auto' v-on:click="autoName(suggest.name)">
            {{suggest.name}}
      </span>
    </div>
</div>
</template>




<script>
        import axios from 'axios';
        export default  {
            methods: {
                searchName() {
                    this.$emit('searchName', this.value)
                    axios
                        .get('https://api.magicthegathering.io/v1/cards?pageSize=5&name='+this.value)
                        .then((response) => {
                            this.auto = JSON.parse(response.request.response).cards
                        })
                },
                showAuto() {
                    document.getElementById('autoName').style.visibility='visible';
                },
                // hideAuto() {
                //     document.getElementById('autoName').style.visibility='hidden';
                // },
                autoName(name) {
                    this.value=name
                    this.$emit('searchName', this.value)
                }

            },
            data() {
                return {
                    value:'',
                    auto:[],
                }
            },
            components: {
                
            }
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