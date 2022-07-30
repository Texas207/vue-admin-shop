<template>
  <div class="dashboard-container">
    <div class="total-layout">
      <el-row :gutter="20">
        <el-col :span="5" v-for="i in 4" :key="i">
          <img :src="imgs[i - 1]" alt="" />
          <div class="title">
            <div class="total-title">{{ totalTitle[i - 1] }}</div>
            <div class="total-value">{{ totalValue[i - 1] }}</div>
          </div>
        </el-col>
      </el-row>
    </div>
    <div class="statistics-layout" style="margin: 40px 120px 0; width: 76%">
      <div
        class="layout-title"
        style="
          color: #606266;
          padding: 15px 20px;
          background: #f2f6fc;
          font-weight: bold;
        "
      >
        订单统计
      </div>
      <el-row>
        <el-col :span="3" style="margin: 0; padding-left: 30px">
          <div class="left" style="height: 422px;">
            <div v-for="(item, index) in contentLeft" :key="index">
              <p
                :style="{
                  color: 'rgb(144, 147, 153)',
                  'font-size': '14px',
                  margin: '0',
                  'margin-top': index > 0 ? '20px' : 0,
                }"
              >
                {{ item.title }}
              </p>
              <p
                style="
                  color: rgb(96, 98, 102);
                  font-size: 24px;
                  padding: 10px 0px;
                  margin: 0;
                "
              >
                {{ item.count }}
              </p>
              <p style="margin: 0">
                <span
                  :style="{
                    color: index % 2 == 0 ? 'red' : 'orange',
                    'font-size': '14px',
                  }"
                  >{{ item.bottom.percent }}</span
                ><span style="font-size: 14px">{{ item.bottom.compare }}</span>
              </p>
            </div>
          </div>
        </el-col>
        <el-col :span="21" style="margin: 0">
          <div style="width: 60vw">
            <VueEcharts
              autoresize
              :option="option"
              style="height: 400px"
            ></VueEcharts>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: "Dashboard",
  computed: {
    ...mapGetters(["name"]),
  },
  data() {
    return {
      option: {
        title: {
          text: "Stacked Area Chart",
        },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "cross",
            label: {
              backgroundColor: "#6a7985",
            },
          },
        },
        legend: {
          data: ["Email", "Union Ads", "Video Ads", "Direct", "Search Engine"],
        },
        toolbox: {
          feature: {
            saveAsImage: {},
          },
        },
        grid: {
          left: "0%",
          right: "4%",
          bottom: "3%",
          containLabel: true,
        },
        xAxis: [
          {
            type: "category",
            boundaryGap: false,
            data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
          },
        ],
        yAxis: [
          {
            type: "value",
          },
        ],
        series: [
          {
            name: "Email",
            type: "line",
            stack: "Total",
            areaStyle: {},
            emphasis: {
              focus: "series",
            },
            data: [120, 132, 101, 134, 90, 230, 210],
          },
          {
            name: "Union Ads",
            type: "line",
            stack: "Total",
            areaStyle: {},
            emphasis: {
              focus: "series",
            },
            data: [220, 182, 191, 234, 290, 330, 310],
          },
          {
            name: "Video Ads",
            type: "line",
            stack: "Total",
            areaStyle: {},
            emphasis: {
              focus: "series",
            },
            data: [150, 232, 201, 154, 190, 330, 410],
          },
          {
            name: "Direct",
            type: "line",
            stack: "Total",
            areaStyle: {},
            emphasis: {
              focus: "series",
            },
            data: [320, 332, 301, 334, 390, 330, 320],
          },
          {
            name: "Search Engine",
            type: "line",
            stack: "Total",
            label: {
              show: true,
              position: "top",
            },
            areaStyle: {},
            emphasis: {
              focus: "series",
            },
            data: [820, 932, 901, 934, 1290, 1330, 1320],
          },
        ],
      },
      imgs: [
        require("@/assets/imgs/1.png"),
        require("@/assets/imgs/2.png"),
        require("@/assets/imgs/3.png"),
        require("@/assets/imgs/4.png"),
      ],
      totalTitle: ["今日订单总数", "今日销售总额", "昨日销售总额", "全部商品"],
      totalValue: ["200", "￥5000.00", "￥5000.00", "53"],
      contentLeft: [
        {
          title: "本月订单总数",
          count: 1563,
          bottom: {
            percent: "+3%",
            compare: "同比上月",
          },
        },
        {
          title: "本周订单总数",
          count: 154,
          bottom: {
            percent: "-2%",
            compare: "同比上周",
          },
        },
        {
          title: "本月销售总额",
          count: 4824,
          bottom: {
            percent: "+5%",
            compare: "同比上月",
          },
        },
        {
          title: "本周销售总额",
          count: 854,
          bottom: {
            percent: "-4%",
            compare: "同比上周",
          },
        },
      ],
    };
  },
};
</script>

<style lang="scss" scoped>
.el-row {
  margin-bottom: 20px;
  &:last-child {
    margin-bottom: 0;
  }
}
.el-col {
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  margin: 10px;
  display: flex;
  text-align: center;
  padding: 10px;
  img {
    width: 60px;
    height: 60px;
  }
  .title {
    height: 60px;
    line-height: 30px;
    margin-left: 10px;
  }
}
.row-bg {
  padding: 10px 0;
  background-color: #f9fafc;
}
.total-layout {
  margin: 40px 120px 0;
}
</style>
