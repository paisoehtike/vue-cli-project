<template>
    <div v-if="data">
        <p><b>Card ID</b> - {{ $route.params.key }}</p>
        <p><b>Application Type</b> - {{ data.application_type }}</p>
        <p><b>Applicant ID</b> - {{ data.applicant_id }}</p>
        <p><b>Member Date</b> - {{ data.member_date }}</p>
        <p><b>End Date</b> - {{ data.end_date }}</p>
        <p><b>Remark</b> - {{ data.remark }}</p>
        <p><b>Type</b> - {{ data.type }}</p>
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
        getDetail() {
            axios.get(`${this.detailUrl}${this.$route.params.key}`)
            .then( res => this.handleRes(res)).catch( res => console.log(res))
        },
        handleRes(res) {
            this.data = JSON.parse(res.data.response)
        }
    },
    created() {
        this.getDetail()
        console.log(`${this.detailUrl}${this.$route.params.key}`)
    }
}
</script>

<style scoped>

</style>