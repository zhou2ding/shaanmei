<template>
  <div class="map-price-container">
    <div class="map-price-form-wrapper">
      <h2 class="map-price-form-title">线路运输单价</h2>
      <div class="map-price-form-row">
        <Multiselect
            v-model="selectedMine"
            :options="mineOptions"
            placeholder="起点"
            :searchable="true"
            :allow-empty="false"
            class="map-form-input"
            popper-class=""
        />
        <input
            class="map-price-form-end-point"
            v-model="searchUnloadPoint"
            placeholder="终点"
        />
        <el-button type="primary" class="form-button" @click="searchStart">查询</el-button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import "@vueform/multiselect/themes/default.scss";
import "element-plus/dist/index.css";
import { ElButton } from "element-plus";
import Multiselect from "@vueform/multiselect";

const selectedMine = ref(null);
const searchUnloadPoint = ref('');
const emit = defineEmits(["onSearch"]);

const mineOptions = ["煤矿A", "煤矿B", "煤矿C"];

const searchStart = () => {
  const searchParams = {
    mine: selectedMine.value,
    endpoint: searchUnloadPoint.value,
  };
  console.log("触发查询事件:", searchParams);
  emit("onSearch", searchParams);
};
</script>

<style lang="scss" scoped>
@import '@/styles/variables/variables.module';

.map-price-container {
  position: absolute;
  left: 70%;
  top: 90px;
}

.map-price-form-title {
  color: #3ad9ff;
  font-size: 28px;
  margin-top: 20px;
}

.map-price-form-wrapper {
  position: absolute;
  top: 20px;
  left: 30px;
  width: 400px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.map-price-form-row {
  display: flex;
  align-items: center;
  gap: 10px;
}

.map-form-input {
  width: 120px;
}

.map-price-form-end-point {
  width: 120px; /* 终点框的宽度 */
  height: calc(var(--ms-border-width, 1px) + var(--ms-font-size, 1rem) * var(--ms-line-height, 1.375) + 2 * var(--ms-py, 0.5rem));
  border-radius: var(--ms-radius, 4px);
  background-color: var(--ms-bg, #FFFFFF);
  border: var(--ms-border-width, 1px) solid var(--ms-border-color, #D1D5DB);
  box-sizing: border-box;
  padding-left: var(--ms-px, 0.875rem);
  font-size: var(--ms-font-size, 1rem);
  line-height: var(--ms-line-height, 1.375);
  outline: none;

  &:focus {
    border: var(--ms-border-width-active, var(--ms-border-width, 1px)) solid var(--ms-border-color-active, #10B981);
    box-shadow: 0 0 0 var(--ms-ring-width, 3px) var(--ms-ring-color, #10B98130);
  }
  &::placeholder {
    color: var(--ms-placeholder-color, #9CA3AF);
  }
}

.form-button {
  white-space: nowrap; /* 确保按钮内容不换行 */
  padding: 8px 20px; /* 调整按钮的内部间距 */
}
</style>