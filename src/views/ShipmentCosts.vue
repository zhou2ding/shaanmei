<template>
  <div class="shipment-costs">
    <Header>
      <h1>运价指数</h1>
    </Header>
    <Search @onSearch="handleSearch"/>
    <div class="chart-container">
      <div class="rect lt"></div>
      <div class="rect rt"></div>
      <div class="rect lb"></div>
      <div class="rect rb"></div>
      <el-button-group class="chart-options">
        <el-button
            v-for="option in chartOptions"
            :key="option"
            @click="changeChart(option)"
            :type="currentChart === option ? 'primary' : 'default'"
        >
          {{ option }}
        </el-button>
      </el-button-group>
      <!-- 折线图部分 -->
      <div class="chart-data" v-if="chartVisible">
        <line-chart :data="chartData"/>
      </div>
    </div>
    <MapRoute />
  </div>
</template>

<script setup>
import {ref} from "vue";
import Search from "@/components/Search/index.vue";
import LineChart from "@/components/LineChart/index.vue";
import {ElButtonGroup, ElButton} from "element-plus";
import Header from '@/components/Header/Header.vue';
import MapRoute from "@/components/RoutePrice/index.vue";

const chartData = ref(null); // 当前折线图数据
const chartOptions = ["综合", "矿区", "煤种"]; // 按钮选项
const currentChart = ref("综合"); // 当前选择的折线图类型
const chartVisible = ref(false); // 控制折线图是否显示

const handleSearch = (searchParams) => {
  console.log("查询参数:", searchParams);
  chartVisible.value = true;

  // 根据查询条件请求数据，这里模拟一个数据结果
  chartData.value = generateMockData(); // 用模拟数据替代实际请求
};

const changeChart = (option) => {
  currentChart.value = option;

  // 根据选项更新数据逻辑
  console.log(`切换到 ${option} 折线图`);
  chartData.value = generateMockData(option); // 替代为根据选项加载不同数据
};

const generateMockData = (type = "综合") => {
  const now = new Date();
  const timestamps = Array.from({length: 60}, (_, idx) => {
    const time = new Date(now - idx * 60000); // 每分钟往前推
    return `${time.getHours()}:${time.getMinutes().toString().padStart(2, "0")}`;
  }).reverse();

  return {
    title: `${type}运价指数时序图`,
    timestamps, // 横轴时间数据
    values: Array.from({length: 60}, () => Math.random() * 100), // 随机数据
  };
};
</script>

<style scoped>
.shipment-costs {
  position: absolute;
  top: 50px;
  left: 200px;
  height: calc(100vh - 50px);
  width: calc(100vw - 200px);
  background: url('@/assets/images/bg.png') no-repeat center center;
  background-size: cover;
}

.chart-container {
  margin: 25px auto;
  padding: 10px 10px;
  border: 1px solid #0079fe;
  background-color: rgba(255, 255, 255, 0.05);
  width: 30%;
  height: auto;
  position: absolute;
  left: 55vh;

  .rect {
    width: 20px;
    height: 20px;
    position: absolute;
    border-top: 4px solid #5fbfff;
    border-left: 4px solid #5fbfff;

    &.lt {
      left: -2px;
      top: -2px;
    }

    &.rt {
      top: -2px;
      right: -2px;
      transform: rotate(90deg);
    }

    &.lb {
      bottom: -2px;
      left: -2px;
      transform: rotate(-90deg);
    }

    &.rb {
      bottom: -2px;
      right: -2px;
      transform: rotate(180deg);
    }
  }
}

.chart-options {
  margin-top: 20px;
  margin-bottom: 20px;
  display: flex;
  justify-content: center;
}

.chart-data {
  margin-top: 10px;
  padding: 0;
}
</style>