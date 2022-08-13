<template>
    <input type='text'  v-model='value' v-on:input="searchName()">
</template>




<script>
        export default  {
            methods: {
                searchName() {
                    this.$emit('searchName', this.value) 
                },

            },
            data() {
            return {
                value:''
            }
        },
            components: {
                
            }
        }
</script>
