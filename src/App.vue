<template>
  <div id="app">
    <h4>
      模式：三个下拉框联动模式；一个下拉框级联模式；&nbsp;&nbsp;
      <button @click="changeAddressMode">当前模式：{{ address_mode }}</button>
    </h4>
    <wlAddress class="my-wl-address" :type="address_mode" :address.sync="address_data"></wlAddress>
  </div>
</template>

<script>
import WlAddress from "./components/address/index.vue";

export default {
  name: "app",
  components: {
    WlAddress
  },
  data() {
    return {
      address_mode: "default", // default普通 cascader级联
      address_data: "" // 选中地址
    };
  },
  methods: {
    changeAddressMode() {
      this.address_mode =
        this.address_mode == "default" ? "cascader" : "default";
    }
  },
  watch: {
    address_data(val) {
      console.log(val);
    }
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
