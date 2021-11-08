<template>
    <div class="mb-3 d-flex justify-content-around nav">
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
}
</script>

<style lang="css" scoped>
    .nav {
        max-width: 500px;
        margin: 0 auto;
    }
</style>