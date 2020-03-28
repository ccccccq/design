<template>
  <el-form :label-width="config.labelWidth + 'px'"
               :label-position="config.labelPosition"
               :size="config.size">
    <draggable
      class="list-group"
      tag="ul"
      v-model="widgetList"
      v-bind="{
        animation: 200,
        group: 'people',
        disabled: false,
        ghostClass: 'ghost'
      }"
      @add="onAdd"
    >
        <el-form-item
          v-for="(element,index) in widgetList"
          :key="element.key"
          v-if="element.key"
          :label="element.name"
          class="list-form-item"
          @click.native.stop="handleWidgetSelect(element)"
          :style="{background: (selectWidget && selectWidget.key == element.key ? '#ccc': '')}"
        >
          <template v-if="element.type == 'input'">
            <el-input
              :style="{width: element.options.width}"
              :placeholder="element.options.placeholder"
              v-model="element.options.defaultValue"
            >
            </el-input>
            <el-button type="text" class="delete-action" @click="onDelete(index)">删除</el-button>
          </template>
        </el-form-item>
    </draggable>
  </el-form>
</template>

<script>
import Draggable from 'vuedraggable'
export default {
  components: {
    Draggable
  },
  props: ['data', 'config', 'select'],
  data () {
    return {
    selectWidget: this.select,
      widgetList: this.data
    }
  },
  methods: {
   handleWidgetSelect (item) {
        this.selectWidget = item
      },
    onAdd (evt) {
      const newIndex = evt.newIndex
      const key = (new Date()).getTime()
      this.$set(this.widgetList, newIndex, {
        ...this.widgetList[newIndex],
        options: {
          ...this.widgetList[newIndex].options
        },
        key
      })
    },
    onDelete(index){
    this.widgetList.splice(index,1);
    }
  },
  watch: {
      // 添加对 select、 slectWidget 的监听
      select (val) {
        this.selectWidget = val
      },
      selectWidget: {
        handler (val) {
          this.$emit('update:select', val)
        },
        deep: true // 为了发现对象内部值的变化
      }
    }
}
</script>
<style lang="scss">
.el-input{
    width:98% !important;
}
.delete-action{
  position: absolute;
  bottom: 5px;
  right: -6px;
}
</style>