<template>
  <form ref="form" class="list-body">
      <div>
        <label for="carid">Car ID</label>
        <input id="carid" type="text" v-model="carid">
      </div>
      <div>
        <label for="make">Manufacturer</label>
        <input id="make" type="text" v-model="make">
      </div>
      <div>
        <label for="model">Model</label>
        <input id="model" type="text" v-model="model">
      </div>
      <div>
        <label for="color">Color</label>
        <input id="color" type="text" v-model="color">
      </div>
      <div>
        <label for="owner">Owner Name</label>
        <input id="owner" type="text" v-model="owner">
      </div>
  </form>
  <button @click="submit">Submit</button>
</template>

<script>
const axios = require('axios').default;

export default {
  data() {
    return {
      carid: null,
      make: null,
      model: null,
      color: null,
      owner: null,
    }
  },
  methods: {
    prepareFormData() {
      let data = {
        'carid': this.carid, 'make': this.make, 'model': this.model,
        'color': this.color, 'owner': this.owner
      }
      this.formData = data
    },
    submit() {
      if(this.$refs.form.reportValidity()) {
        this.prepareFormData()
        axios.post('http://13.76.94.34:8080/api/addcar', this.formData, {
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
