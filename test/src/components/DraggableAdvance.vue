<template>
  <el-row :gutter="50">
    <el-col :span="6">
      <h3>Draggable 1</h3>
      <draggable
        class="list-group"
        tag="ul"
        v-model="componentList"
      >
          <li
            class="list-group-item"
            v-for="element in componentList"
            :key="element.type"
          >
            {{ element.name }}
          </li>
      </draggable>

    </el-col>
    <el-col :span="6">
      <h3>Draggable 2</h3>
      <draggable
        class="list-group"
        tag="ul"
        v-model="widgetList"
        @add="onAdd"
      >
          <li
           class="list-group-item"
           v-for="element in widgetList"
           :key="element.key"
           v-if="element.key"
          >
            {{ element.name }}
          </li>
      </draggable>
    </el-col>
    <el-col :span="6">
      <h3>List 1</h3>
      <pre style="text-align: start;background: #f3f3f3;">{{JSON.stringify(list1, null, 2)}}</pre>
    </el-col>
    <el-col :span="6">
      <h3>List 2</h3>
      <pre style="text-align: start;background: #f3f3f3;">{{JSON.stringify(list2, null, 2)}}</pre>
    </el-col>
  </el-row>
</template>

<script>
import Draggable from "vuedraggable"

export default {
  components: {
    Draggable
  },
  data () {
    return {
      list1: [
        { name: "Jesus", id: 1 },
        { name: "Paul", id: 2 },
        { name: "Peter", id: 3 }
      ],
      list2: [
        { name: "Luc", id: 5 },
        { name: "Thomas", id: 6 },
        { name: "John", id: 7 }
      ],
      dragOptions1: {
              animation: 200,
              group:{ name:'people', pull:'clone',put:false}, // 配置项
                //pull：pull 用来定义从这个列表容器移动出去的设置，true:列表容器内的列表元素可以被移出；false：列表容器内的列表元素不可以被移出；'clone'：列表元素移出，移动的为该元素的副本；
                // put：put 用来定义往这个列表容器放置列表元素的的设置，true:列表容器可以从其他列表容器内放入列表元素；false：与 true 相反
              disabled: false,
              ghostClass: 'ghost'
            },
       dragOptions2: {
              animation: 200,
              group: 'people',
              disabled: false,
              ghostClass: 'ghost'
      }
    }
  },
     methods: {
   onAdd (evt) {
      alert(evt.oldIndex + '->' + evt.newIndex)
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
/* ... */
</style>