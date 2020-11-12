<template>
    <div>
        <table v-if="carOrCertificate == 'car'">
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

        <table v-else>
            <tr>
                <th>Card ID</th>
                <th>Application Type</th>
                <th>Applicant ID</th>
                <th>Member Date</th>
                <th>End Date</th>
                <th>Type</th>
            </tr>
            <tr v-for="value in data" :key="value.card_id">
                <router-link :to="'/detail/' + value.card_id" tag="td">{{ value.card_id }}</router-link>
                <td>{{ value.application_type }}</td>
                <td>{{ value.applicant_id }}</td>
                <td>{{ value.member_date }}</td>
                <td>{{ value.end_date }}</td>
                <td>{{ value.type }}</td>
            </tr>
        </table>
    </div>
</template>

<script>
const axios = require('axios').default;
import apiConfigMixins from '../mixins/apiConfigMixins'

export default {
    mixins: [apiConfigMixins],
    data() {
        return {
            data: null,
        }
    },
    methods: {
        getAllCars() {
            axios.get(this.getUrl)
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