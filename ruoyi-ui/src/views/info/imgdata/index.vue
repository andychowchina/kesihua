<template>
  <div class="app-container">
    <el-row :gutter="10" class="mb8">
      <el-col :span="1.5">
        <el-button type="primary" plain icon="el-icon-plus" size="mini"
          >新增</el-button
        >
      </el-col>
    </el-row>

    <div>
      <div class="demo-image">
        <div
          class="block"
          v-for="(img, key) in imgs"
          :key="key"
          @click="select_cv(img)"
        >
          <span class="demonstration">{{ img.name }}</span>
          <el-image
            style="width: 150px; height: 150px"
            :src="img.url"
            :fit="img.name"
          ></el-image>
        </div>
      </div>
    </div>
    <h1>自定义</h1>
    <div style="margin-bottom: 1em">
      <el-button type="primary">保存</el-button>
    </div>
    <el-row>
      <el-col :span="12">
        <div class="grid-content">1</div>
      </el-col>
      <el-col :span="12">
        <div class="grid-content">
          <div id="main" style="height: 500px"></div>
        </div>
      </el-col>
    </el-row>

    <h1>大屏</h1>
    <draggable
      :list="imgs"
      animation="340"
      class="drag-wrapper"
    >
      <div class="item" v-for="element in imgs" :key="element.id">{{element.name}}</div>
    </draggable>
  </div>
</template>

<script>
import * as echarts from "echarts";
import draggable from "vuedraggable";

export default {
  components: { draggable },
  name: "imgdata",
  data() {
    return {
      imgs: [
        {
          url:
            "https://cdn.jsdelivr.net/gh/apache/echarts-website@asf-site/examples/data/thumb/line-simple.webp?_v_=1612615474746",
          name: "基础折线图",
          title: "Basic Line Chart",
        },
        {
          url:
            "https://cdn.jsdelivr.net/gh/apache/echarts-website@asf-site/examples/data/thumb/line-smooth.webp?_v_=1612615474746",
          name: "基础平滑折线图",
          title: "Smoothed Line Chart",
        },
      ],
      options: [
        {
          name: "Basic Line Chart",
          option: {
            xAxis: {
              type: "category",
              data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
            },
            yAxis: {
              type: "value",
            },
            series: [
              {
                data: [150, 230, 224, 218, 135, 147, 260],
                type: "line",
              },
            ],
          },
        },
        {
          name: "Smoothed Line Chart",
          option: {
            xAxis: {
              type: "category",
              data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
            },
            yAxis: {
              type: "value",
            },
            series: [
              {
                data: [820, 932, 901, 934, 1290, 1330, 1320],
                type: "line",
                smooth: true,
              },
            ],
          },
        },
      ],
    };
  },
  mounted() {},
  methods: {
    init_cv(op) {
      var chartDom = document.getElementById("main");
      var myChart = echarts.init(chartDom);
      var option;

      option = op;

      option && myChart.setOption(option);
    },
    select_cv(s) {
      var _op = "";
      this.options.forEach((el) => {
        if (el.name == s.title) {
          _op = el.option;
          this.init_cv(_op);
          return;
        }
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.demo-image .demonstration,
.demo-image__error .demonstration,
.demo-image__placeholder .demonstration {
  display: block;
  color: #8492a6;
  font-size: 14px;
  margin-bottom: 20px;
}
.demo-image .block,
.demo-image__error .block,
.demo-image__placeholder .block {
  padding: 30px 0;
  text-align: center;
  border-right: 1px solid #eff2f6;
  display: inline-block;
  margin: 1em;
  padding: 1em;
  box-sizing: border-box;
  vertical-align: top;
  cursor: pointer;
}
.demo-image .block:hover {
  border: 1px solid #1890ff;
  border-radius: 1em;
}
</style>
