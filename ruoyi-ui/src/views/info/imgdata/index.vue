<template>
  <div class="app-container">
    <el-row :gutter="10" class="mb8">
      <el-col :span="1.5">
        <el-button type="primary" plain icon="el-icon-plus" size="mini"
          >新增</el-button
        >
      </el-col>
    </el-row>
    <!--  -->
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
    <!--  -->
    <h1>自定义</h1>
    <div style="margin-bottom: 1em">
      <el-button type="primary" @click="init_big_cv_done">保存</el-button>
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
    <!--  -->
    <h1>大屏</h1>
    <div style="margin-bottom: 1em">
      <el-button type="primary">保存</el-button>
    </div>
    <div class="drag-pr-cv">
      <vue-drag-resize
        :parent="true"
        :w="300"
        :h="300"
        :x="img.x"
        :y="img.y"
        @resizing="resize_f"
        :onResizeStart="onResizeStartCallback"
        v-for="(img, key) in options"
        :key="key"
      >
        <div :ref="img.name" :data-name="img.name" class="target-cv"></div>
      </vue-drag-resize>
    </div>
  </div>
</template>

<script>
import * as echarts from "echarts";
import VueDragResize from "vue-draggable-resizable";
import "vue-draggable-resizable/dist/VueDraggableResizable.css";

export default {
  components: { VueDragResize },
  name: "imgdata",
  data() {
    return {
      target: undefined,
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
          x: 0,
          y: 0,
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
          x: 400,
          y: 0,
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
    init_big_cv(op) {
      var chartDom = this.$refs[op.name][0];
      chartDom.style.width = "100%";
      chartDom.style.height = "100%";
      var myChart = echarts.init(chartDom);
      var option;
      option = op.option;
      option && myChart.setOption(option);
    },
    init_big_cv_done() {
      this.options.forEach((o, i) => {
        this.init_big_cv(o);
      });
    },
    resize_f(x, y, width, height) {
      this.$refs[this.target][0].getElementsByTagName("canvas")[0].style.width =
        width + "px";
      this.$refs[this.target][0].getElementsByTagName(
        "canvas"
      )[0].style.height = height + "px";
    },
    onResizeStartCallback(handle, ev) {
      this.target = ev.target.parentElement
        .getElementsByClassName("target-cv")[0]
        .getAttribute("data-name");
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

.drag-pr-cv {
  height: calc(100vh);
  width: 100%;
  position: relative;
  border: 1px solid #ddd;
}
</style>
