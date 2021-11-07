<template>
    <div class="mb-5 nav">
        <b-button  variant="info" v-on:click="changeView(1)">TABLE</b-button>
        <b-button  variant="info" v-on:click="changeView(2)">FORM</b-button>
    </div>
</template>

<script>
export default {
    name: 'NavBar',
    methods: {
        changeView(arg){
            this.$emit('changeView', arg)
        },
    },
    data: function(){
        return{
            tableNav: '',
            formNav: ''
        }
    }
}
</script>

<style lang="css" scoped>
    .nav {
        display: flex;
        justify-content: space-evenly
    }
</style>