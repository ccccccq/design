<template>
  <el-container class="fm-container">
    <el-aside width="300px" class="fm-left">
      <draggable
        class="list-group"
        tag="ul"
        v-model="componentList"
        v-bind="{
          animation: 200,
          group:{ name:'people', pull:'clone',put:false},
          disabled: false,
          ghostClass: 'ghost'
        }"
      >
          <li
            class="list-group-item"
            v-for="element in componentList"
            :key="element.type"
          >
            {{ element.name }}
          </li>
      </draggable>
    </el-aside>
    <el-main class="fm-main">
     <widget-form :data="widgetList" :config="formConfig"  :select.sync="widgetSelect"></widget-form>
    </el-main>
    <el-aside width="300px" class="fm-right">
      <el-tabs v-model="activeName" >
        <el-tab-pane label="字段配置" name="widget">
          <widget-config :data="widgetSelect" v-if="widgetSelect"></widget-config>
        </el-tab-pane>
        <el-tab-pane label="表单配置" name="form">
          <form-config :data="formConfig"></form-config>
        </el-tab-pane>
      </el-tabs>
    </el-aside>
  </el-container>
</template>

<script>
import Draggable from 'vuedraggable'
import WidgetForm from './WidgetForm'
import FormConfig from './FormConfig'
import WidgetConfig from './WidgetConfig'

export default {
  components: {
    Draggable,
    WidgetForm,
    FormConfig,
    WidgetConfig
  },
  data () {
    return {
          widgetSelect: null,
          activeName: 'widget',
          formConfig: {
            labelWidth: '100px',
            labelPosition: 'top',
            size: 'small'
          },
      componentList: [
        {
          type: 'input',
          name: '单行文本',
          options: {
            width: '100%',
            defaultValue: '',
            placeholder: ''
          }
        }
      ],
      widgetList: [],
      widgetSelect: null
    }
  },
  methods: {
    onAdd (evt) {
      // evt： 事件对象，具体可以参考上个实验《2.4 拖拽事件》中有详细描述
      const newIndex = evt.newIndex
      const key = (new Date()).getTime()
      this.$set(this.widgetList, newIndex, {
        ...this.widgetList[newIndex],
        options: {
          ...this.widgetList[newIndex].options
        },
        key
      })
    }
  }
}
</script>

<style lang="scss">
/* 添加样式 */
.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}
.list-group {
  min-height: 20px;
  list-style: none;
}
.list-group-item {
  cursor: move;
  height: 30px;
  line-height: 30px;
  border: 1px solid #ccc;
}
.list-form-item{
  border: 1px dashed blue;
  padding: 5px;

  &.el-form-item{
    margin: 2px;
  }
}
/* ... */
</style>
