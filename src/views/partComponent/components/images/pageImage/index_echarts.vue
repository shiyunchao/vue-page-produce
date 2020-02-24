<template>
  <div
    class="testComponent_one"
    style="width:100%;height:100%"
  >

    <!-- :style="{
    color: currentWidgetStyleFields.color.formModel,
    fontSize: currentWidgetStyleFields.fontSize.formModel
  }" -->
        <!-- src="../../images/TitleChildOne_icon.jpg" -->
    <!-- <img
        :src="fakeData"
        style="width:100%;height:100%"
    /> -->
    <div :id="`myChart_${uuid}`" style="width:100%;height:100%"></div>
  </div>
</template>

<script>
import echarts from 'echarts'
import { mapState } from 'vuex'
export default {
  props: {
    uuid: {
      type: String,
      required: true
    }
  },
  data() {
    return {}
  },
  computed: {
    ...mapState("partComponent", ["widgetList"]),
    currentWidget() {
      return this.widgetList.find(v => v.uuid === this.uuid)
    },
    currentWidgetStyleFields() {
      return this.currentWidget.styleFields
    },
    currentWidgetFields() {
      return this.currentWidget.fields
    },
    fakeData() {
      return this.currentWidgetFields.url.formModel
    },
  },
  mounted(){
    this.$nextTick(() => {
      this.drawLine();
    })
  },
  methods: {
    drawLine(){
        // 基于准备好的dom，初始化echarts实例
        let myChart = echarts.init(document.getElementById('myChart_'+this.uuid))
        // 绘制图表
        myChart.setOption({
            title: { text: '在Vue中使用echarts' },
            tooltip: {},
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        });
    }
  }
}
</script>

<style>
.testComponent_one {
  width: 100%;
  height: 100%;
}
</style>
