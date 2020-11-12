<template>
  <form v-if="carOrCertificate == 'car'" ref="form" class="list-body">
      <!-- <div v-for="item of input_list" :key="item">
        <label for="carid">{{ item.label }}</label>
        <TestingInput
          v-model:name="item.id"
          :id="item.id"
        ></TestingInput>
      </div> -->
      <div>
        <label for="carid">Car ID</label>
        <TestingInput
          v-model:name="carid"
          :id="'carid'"
        ></TestingInput>
      </div>
      <div>
        <label for="make">Manufacturer</label>
        <TestingInput
          v-model:name="make"
          :id="'make'"
        ></TestingInput>
      </div>
      <div>
        <label for="model">Model</label>
        <TestingInput
          v-model:name="model"
          :id="'model'"
        ></TestingInput>
      </div>
      <div>
        <label for="color">Color</label>
        <TestingInput
          v-model:name="color"
          :id="'color'"
        ></TestingInput>
      </div>
      <div>
        <label for="owner">Owner Name</label>
        <TestingInput
          v-model:name="owner"
          :id="'owner'"
        ></TestingInput>
      </div>
  </form>

  <form v-else ref="form" class="list-body">
      <!-- <div v-for="item of input_list" :key="item">
        <label for="carid">{{ item.label }}</label>
        <TestingInput
          v-model:name="item.id"
          :id="item.id"
        ></TestingInput>
      </div> -->
      <div>
        <label for="cardid">Card ID</label>
        <TestingInput
          v-model:name="cardid"
          :id="'cardid'"
        ></TestingInput>
      </div>
      <div>
        <label for="applicationtype">Application Type</label>
        <TestingInput
          v-model:name="applicationtype"
          :id="'applicationtype'"
        ></TestingInput>
      </div>
      <div>
        <label for="applicantid">Applicant ID</label>
        <TestingInput
          v-model:name="applicantid"
          :id="'applicantid'"
        ></TestingInput>
      </div>
      <div>
        <label for="memberdate">Member Date</label>
        <TestingInput
          v-model:name="memberdate"
          :id="'memberdate'"
        ></TestingInput>
      </div>
      <div>
        <label for="enddate">End Date</label>
        <TestingInput
          v-model:name="enddate"
          :id="'enddate'"
        ></TestingInput>
      </div>
      <div>
        <label for="remark">Remark</label>
        <TestingInput
          v-model:name="remark"
          :id="'remark'"
        ></TestingInput>
      </div>
  </form>
  <button @click="submit">Submit</button>
</template>

<script>
const axios = require('axios').default;
import TestingInput from '../components/TestingInput'
import apiConfigMixins from '../mixins/apiConfigMixins'

export default {
  mixins: [apiConfigMixins],
  components: {
    TestingInput
  },
  data() {
    return {
      carid: null,
      make: null,
      model: null,
      color: null,
      owner: null,

      cardid: null,
      applicationtype: null,
      applicantid: null,
      memberdate: null,
      enddate: null,
      remark: null,
      // input_list: [
      //   {
      //     id: 'carid',
      //     label: 'Car ID'
      //   },
      //   {
      //     id: 'make',
      //     label: 'Manufacturer'
      //   },
      //   {
      //     id: 'model',
      //     label: 'Model'
      //   },
      //   {
      //     id: 'color',
      //     label: 'Color'
      //   },
      //   {
      //     id: 'owner',
      //     label: 'Owner'
      //   },
      // ]
    }
  },
  methods: {
    prepareFormData() {
      if(this.carOrCertificate == 'car') {
        this.formData = {
          'carid': this.carid, 'make': this.make, 'model': this.model,
          'color': this.color, 'owner': this.owner
        }
      } else {
          this.formData = {
          'card_id': this.cardid, 'application_type': this.applicationtype, 'applicant_id': this.applicantid,
          'member_date': this.memberdate, 'end_date': this.enddate, 'remark': this.remark
        }
      }
    },
    submit() {
      if(this.$refs.form.reportValidity()) {
        this.prepareFormData()
        axios.post(this.postUrl, this.formData, {
          headers: {
            'Content-Type': 'application/json'
          }
        })
        .then(res => this.handleResponse(res)).catch( res => console.log(res))
      }
    },
    handleResponse(res) {
      if(res.status === 200) {
        this.$router.push('/')
      }
    }
  }
}
</script>

<style scoped>
div {
  margin-top: 20px;
}
label {
  display: inline-block;
  width: 200px;
  text-align: right;
  padding-right: 20px;
}
input {
  margin-left: 20px;
}
button {
  margin-top: 60px;
  width: 90px;
  padding: 10px 0;
  border: 1px solid #3e3e3e;
  background: none;
  border-radius: 5px;
}
button:hover {
  background: #42b983;
  border-color: #fff;
  color: #fff;
  cursor: pointer;
}
</style>
