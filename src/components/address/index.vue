<template>
  <div class="wl-address">
    <el-select
      @change="provinceChange"
      v-model="province_act"
      placeholder="请选择省份"
      value-key="code"
      :size="size"
    >
      <el-option
        v-for="item in provinces"
        :key="item.code"
        :label="item.name"
        :value="item"
      >
      </el-option>
    </el-select>
    <el-select
      v-model="city_act"
      :size="size"
      value-key="code"
      placeholder="请选择城市"
      @change="citysChange"
    >
      <el-option
        v-for="item in citys"
        :key="item.code"
        :label="item.name"
        :value="item"
      >
      </el-option>
    </el-select>
    <el-select
      v-model="county_act"
      :size="size"
      value-key="code"
      placeholder="请选择区/县"
      @change="countysChange"
    >
      <el-option
        v-for="item in countys"
        :key="item.code"
        :label="item.name"
        :value="item"
      >
      </el-option>
    </el-select>
  </div>
</template>
<script>
import { getProvince, getCity, getCounty } from "./address.js"; // 导入获取省市县

export default {
  name: "wlAddress",
  data() {
    return {
      provinces: [], // 省份
      citys: [], // 市
      countys: [], // 县
      province_act: {
        code: "",
        name: ""
      }, // 当前省
      city_act: {
        code: "",
        name: ""
      }, // 当前省
      county_act: {
        code: "",
        name: ""
      } // 当前省
    };
  },
  props: {
    // 输入框尺寸
    size: {
      type: String,
      default: ""
    },
    // 默认数据
    address: {
      type: String,
      default: ""
    }
  },
  created() {
    this.provinces = getProvince();
    this.analysisDefaultAddress();
  },
  methods: {
    // 省份更改
    provinceChange(val) {
      this.city_act = {
        code: "",
        name: ""
      };
      this.county_act = {
        code: "",
        name: ""
      };
      this.countys = [];
      this.citys = getCity(val);
    },
    // 城市更改
    citysChange(val) {
      this.county_act = {
        code: "",
        name: ""
      };
      this.countys = getCounty(val);
    },
    // 县更改
    countysChange(val) {
      let string_address = JSON.stringify([
        this.province_act,
        this.city_act,
        this.county_act
      ]);
      this.$emit("update:address", string_address);
    },
    // 解析默认地址
    analysisDefaultAddress() {
      if (!this.address) return;
      let address = "";
      try {
        address = JSON.parse(this.address) || [];
      } catch (error) {
        console.log("地址信息不合规范:" + error);
      }
      if (address instanceof Array) {
        [
          this.province_act = {},
          this.city_act = {},
          this.county_act = {}
        ] = address;

        if (this.province_act.code) {
          this.citys = getCity(this.province_act);
        }

        if (this.city_act.code) {
          this.countys = getCounty(this.city_act);
        }
      }
    }
  },
  watch: {
    address(val) {
      this.analysisDefaultAddress();
    }
  }
};
</script>

<style lang="css">
.wl-address{
  display: flex;
  justify-content: space-between;
}

.wl-address .el-select{
  flex: 0.31;
}
</style>
