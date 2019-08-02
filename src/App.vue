<template>
  <div id="app">
    <wlAddress class="my-wl-address" :address.sync="address_data"></wlAddress>
  </div>
</template>

<script>
// import wlAddress from "./components/address/index.vue";

export default {
  name: "app",
  data() {
    return {
      address_data: ""
    };
  },
  watch: {
    address_data(val) {
      console.log(val);
    }
  },
  components: {
    // wlAddress
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.my-wl-address {
  margin: 160px auto;
  width: 540px;
}
</style>
