<template>
    <div class="shipment-costs-search-container">
      <img src="@/assets/images/card.png" alt="404">
      <div class="shipment-costs-search-form-wrapper">
        <h2 class="shipment-costs-search-form-title">运价指数查询</h2>
        <div class="shipment-costs-search-form-item">
          <el-config-provider :locale="zhCn">
            <el-date-picker
                v-model="selectedDate"
                type="date"
                placeholder="选择日期"
                class="form-input"
                popper-class=""
                :locale="zhCn"
            />
          </el-config-provider>
        </div>
        <div class="shipment-costs-search-form-item">
          <Multiselect
              v-model="selectedMine"
              :options="mineOptions"
              placeholder="请输入装货煤矿"
              :searchable="true"
              :allow-empty="false"
              class="form-input"
              popper-class=""
          />
        </div>
        <div class="shipment-costs-search-form-item">
          <Multiselect
              v-model="selectedPort"
              :options="portOptions"
              placeholder="请输入卸货点"
              :searchable="true"
              :allow-empty="false"
              class="form-input"
              popper-class=""
          />
        </div>
        <div class="shipment-costs-search-form-item">
          <Multiselect
              v-model="selectedCoalType"
              :options="coalTypeOptions"
              placeholder="请输入煤种种类"
              :searchable="true"
              :allow-empty="false"
              class="form-input"
              popper-class="custom-popper"
          />
        </div>
        <div class="shipment-costs-search-form-item">
          <el-button type="primary" class="form-button" @click="emitSearch">查询</el-button>
        </div>
      </div>
    </div>
</template>

<script setup>
import {ref} from "vue";
import "@vueform/multiselect/themes/default.scss";
import "element-plus/dist/index.css";
import {ElDatePicker, ElButton, ElConfigProvider} from "element-plus";
import Multiselect from "@vueform/multiselect";
import zhCn from 'element-plus/es/locale/lang/zh-cn';

const selectedDate = ref(null);
const selectedMine = ref(null);
const selectedPort = ref(null);
const selectedCoalType = ref(null);
const emit = defineEmits(["onSearch"]);

const mineOptions = ["煤矿A", "煤矿B", "煤矿C"];
const portOptions = ["卸货点A", "卸货点B", "卸货点C"];
const coalTypeOptions = ["煤种A", "煤种B", "煤种C"];

const emitSearch = () => {
  const searchParams = {
    date: selectedDate.value,
    mine: selectedMine.value,
    port: selectedPort.value,
    coalType: selectedCoalType.value,
  };
  console.log("触发查询事件:", searchParams);
  emit("onSearch", searchParams);
};
</script>

<style lang="scss" scoped>
@import '@/styles/variables/variables.module';

img {
  width: 360px;
  height: 340px;
  margin-top: 20px;
}

.shipment-costs-search-container {
  position: absolute;
  left: 50px;
  top: 90px;
}

.shipment-costs-search-form-title {
  color: #3ad9ff;
  font-size: 24px;
  margin-top: 20px;
}

.shipment-costs-search-form-wrapper {
  position: absolute;
  top: 20px;
  left: 20px;
  width: 300px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.shipment-costs-search-form-item {
  display: flex;
  flex-direction: column;
}

.form-input {
  width: 100%;
}

.form-button {
  width: 100%;
}

</style>