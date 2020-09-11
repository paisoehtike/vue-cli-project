<template>
    <div v-if="data">
        <p><b>Car ID</b> - {{ $route.params.key }}</p>
        <p><b>Owner</b> - {{ data.owner }}</p>
        <p><b>Model</b> - {{ data.model }}</p>
        <p><b>Manufacturer</b> - {{ data.make }}</p>
        <p><b>Color</b> - {{ data.color }}</p>
    </div>
</template>

<script>
const axios = require('axios').default;

export default {
    data() {
        return {
            data: null,
        }
    },
    methods: {
        getDetail() {
            axios.get('http://13.76.94.34:8080/api/query/' + this.$route.params.key)
            .then( res => this.handleRes(res)).catch( res => console.log(res))
        },
        handleRes(res) {
            this.data = JSON.parse(res.data.response)
        }
    },
    created() {
        this.getDetail()
    }
}
</script>

<style scoped>

</style>