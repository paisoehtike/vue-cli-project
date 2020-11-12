<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">
        {{carOrCertificate == 'car' ? 'Cars' : 'Certificates'}}
      </router-link> |
      <router-link to="/about">
        {{carOrCertificate == 'car' ? 'Create New Cars' : 'Create New Certificate'}}
      </router-link>
    </div>
    <router-view/>
  </div>
</template>

<script>
import apiConfigMixins from './mixins/apiConfigMixins'

export default {
  mixins: [apiConfigMixins],
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
