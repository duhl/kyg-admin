<template>
  <div class="board-column">
    <div class="board-column-header">
      {{ headerText }}
    </div>
    <draggable
      :list="list"
      v-bind="$attrs"
      class="board-column-content"
      :set-data="setData"
      :group="{ name: 'lunbo', pull: 'clone', put: false }"
    >
      <div
        v-for="(element, index) in list"
        :key="element.id"
        :class="['board-item', { active: index == active }]"
        @click="onActive(index, element)"
      >
        <!-- <span v-for="(item, lbIndex) in lunboList" :key="`lb${lbIndex}`">
          {{ item }}
        </span> -->
        <el-carousel
          v-if="
            lunboList.length &&
              element.type == 'lunbo' &&
              headerText == 'Working'
          "
          trigger="click"
          height="60px"
        >
          <el-carousel-item
            v-for="(item, lbIndex) in lunboList"
            :key="`lb${lbIndex}`"
          >
            <!-- <h3 class="small">{{ item }}</h3> -->
            <img :src="item.images" />
          </el-carousel-item>
        </el-carousel>
        <span v-else>{{ element.name }}</span>
        <div
          v-if="element.type == 'lunbo' && headerText == 'Working'"
          class="icon"
        >
          <span class="el-icon-top" @click="sortUp(index, list)" />
          <span class="el-icon-bottom" @click="sortDown(index, list)" />
        </div>
      </div>
    </draggable>
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "DragKanbanDemo",
  components: {
    draggable
  },
  props: {
    headerText: {
      type: String,
      default: "Header"
    },
    active: {
      type: Number,
      default: null
    },
    options: {
      type: Object,
      default() {
        return {};
      }
    },
    list: {
      type: Array,
      default() {
        return [];
      }
    },
    lunboList: {
      type: Array,
      default() {
        return [];
      }
    },
    sortUp: {
      type: Function,
      default() {
        return () => {};
      }
    },
    sortDown: {
      type: Function,
      default() {
        return () => {};
      }
    },
    onActive: {
      type: Function,
      default() {
        return () => {};
      }
    }
  },
  methods: {
    setData(dataTransfer) {
      console.info("dataTransfer", dataTransfer);
      // to avoid Firefox bug
      // Detail see : https://github.com/RubaXa/Sortable/issues/1012
      dataTransfer.setData("Text", "");
    }
  }
};
</script>
<style lang="scss" scoped>
.board-column {
  min-width: 300px;
  min-height: 100px;
  height: auto;
  overflow: hidden;
  background: #f0f0f0;
  border-radius: 3px;

  .board-column-header {
    height: 50px;
    line-height: 50px;
    overflow: hidden;
    padding: 0 20px;
    text-align: center;
    background: #333;
    color: #fff;
    border-radius: 3px 3px 0 0;
  }

  .board-column-content {
    height: auto;
    overflow: hidden;
    border: 10px solid transparent;
    min-height: 60px;
    display: flex;
    justify-content: flex-start;
    flex-direction: column;
    align-items: center;

    .board-item {
      cursor: pointer;
      width: 100%;
      height: 70px;
      margin: 5px 0;
      background-color: #fff;
      text-align: left;
      line-height: 54px;
      padding: 5px 10px;
      box-sizing: border-box;
      box-shadow: 0px 1px 3px 0 rgba(0, 0, 0, 0.2);
      position: relative;
      .icon {
        width: 18px;
        height: 100%;
        padding: 10px 0;
        // border: 1px solid red;
        position: absolute;
        right: 0;
        top: 0;
        span {
          float: left;
          clear: left;
        }
        span:nth-of-type(1) {
          margin-bottom: 20px;
        }
      }
    }
    .board-item.active {
      // border: 1px solid red;
    }
  }
}
</style>
