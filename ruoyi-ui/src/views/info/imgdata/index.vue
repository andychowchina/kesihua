<template>
  <div class="app-container">
    <el-row :gutter="10" class="mb8">
      <el-col :span="1.5">
        <el-button
          type="primary"
          plain
          icon="el-icon-plus"
          size="mini"
          >新增</el-button
        >
      </el-col>
    </el-row>

    <div>
      <div class="demo-image">
        <div class="block" v-for="(img,key) in imgs" :key="key">
          <span class="demonstration">{{ img.name }}</span>
          <el-image
            style="width: 150px; height: 150px"
            :src="img.url"
            :fit="img.name"
          ></el-image>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import * as echarts from 'echarts/core';
import {
    GridComponent
} from 'echarts/components';
import {
    LineChart
} from 'echarts/charts';
import {
    CanvasRenderer
} from 'echarts/renderers';

export default {
  name: "imgdata",
  data() {
    return {
      imgs: [
        {
          url:
            "https://cdn.jsdelivr.net/gh/apache/echarts-website@asf-site/examples/data/thumb/line-simple.webp?_v_=1612615474746",
          name: "基础折线图",
        },
        {
          url:
            "https://cdn.jsdelivr.net/gh/apache/echarts-website@asf-site/examples/data/thumb/line-smooth.webp?_v_=1612615474746",
          name: "基础平滑折线图",
        },
      ],
    };
  },
  methods: {},
};
</script>

<style lang="scss" scoped>
.demo-image .demonstration, .demo-image__error .demonstration, .demo-image__placeholder .demonstration {
    display: block;
    color: #8492a6;
    font-size: 14px;
    margin-bottom: 20px;
}
.demo-image .block, .demo-image__error .block, .demo-image__placeholder .block {
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
.demo-image .block:hover{
    border: 1px solid #1890ff;
    border-radius: 1em;
}
</style>
