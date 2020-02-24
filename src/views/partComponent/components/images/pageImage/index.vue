<template>
  <div
    class="testComponent_one"
  >

    <!-- :style="{
    color: currentWidgetStyleFields.color.formModel,
    fontSize: currentWidgetStyleFields.fontSize.formModel
  }" -->
        <!-- src="../../images/TitleChildOne_icon.jpg" -->

        <!-- :style="{
          width: currentWidth,
          height: currentHeight
        }" -->
    <img
        :src="fakeData"
        style="width:100%; height:100%;"
    />
  </div>
</template>

<script>
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
    currentWidth() {
      return this.currentWidgetStyleFields.width.formModel ? this.currentWidgetStyleFields.width.formModel + 'px' : '100%'
    },
    currentHeight() {
      return this.currentWidgetStyleFields.height.formModel ? this.currentWidgetStyleFields.height.formModel + 'px' : '100%'
    },
    currentWidgetFields() {
      return this.currentWidget.fields
    },
    fakeData() {
      return this.currentWidgetFields.url.formModel
    },
  }
}
</script>

<style>
.testComponent_one {
  width: 100%;
  height: 100%;
}
</style>
