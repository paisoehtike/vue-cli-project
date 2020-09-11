<template>
    <div>
        <table>
            <tr>
                <th>Key</th>
                <th>Owner</th>
                <th>Model</th>
                <th>Color</th>
                <th>Manufacturer</th>
            </tr>
            <tr v-for="value in data" :key="value.Key">
                <router-link :to="'/detail/' + value.Key" tag="td">{{ value.Key }}</router-link>
                <!-- <td>{{ value.Key }}</td> -->
                <td>{{ value.Record.owner }}</td>
                <td>{{ value.Record.model }}</td>
                <td>{{ value.Record.color }}</td>
                <td>{{ value.Record.make }}</td>
            </tr>
        </table>
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
        getAllCars() {
            axios.get('http://13.76.94.34:8080/api/queryallcars')
            .then( res => this.handleRes(res)).catch( res => console.log(res))
        },
        handleRes(res) {
            this.data = JSON.parse(res.data.response)
        }
    },
    created() {
        this.getAllCars()
    }
}
</script>

<style scoped>
    table {
        margin: auto;
    }
    tr {
        height: 30px;
    }
    th, td {
        width: 100px;
    }
</style>