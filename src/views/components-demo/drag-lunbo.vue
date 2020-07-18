<template>
  <div class="components-container board">
    <Lunbo
      :key="1"
      :list="list1"
      :group="group"
      class="lunbo todo"
      header-text="Todo"
    />
    <Lunbo
      :key="2"
      :list="list2"
      :group="group"
      :sort-up="handleSortUp"
      :sort-down="handleSortDown"
      class="lunbo working"
      header-text="Working"
    />
    <Lunbo
      :key="3"
      :list="list3"
      :group="group"
      class="lunbo done"
      header-text="Done"
    />
  </div>
</template>
<script>
import Lunbo from "@/components/Lunbo";

export default {
  name: "DragLunboDemo",
  components: {
    Lunbo
  },
  data() {
    return {
      group: "mission",
      list1: [
        { name: "轮播图", id: 1, type: "lunbo" }
        /* { name: "Mission", id: 2 },
        { name: "Mission", id: 3 },
        { name: "Mission", id: 4 } */
      ],
      list2: [
        { name: "图片", id: 5, tyle: "template" },
        { name: "文字", id: 6, tyle: "template" }
        /* { name: "文字", id: 7 } */
      ],
      list3: [
        /* { name: "Mission", id: 8 },
        { name: "Mission", id: 9 },
        { name: "Mission", id: 10 } */
      ]
    };
  },
  watch: {
    list1(val) {
      console.log("list1-change,", val);
    },
    list2(val) {
      console.log("list2-change,", val);
    },
    list3(val) {
      console.log("list3-change,", val);
    }
  },
  methods: {
    handleSortUp(index, list) {
      console.info("upArrow,", index);
      if (index) {
        console.info("upArrow-set,", index, list);
        let curItem = list.splice(index, 1);
        console.info("upArrow-delete,", curItem);
        list.splice(index - 1, 0, ...curItem);
      }
    },
    handleSortDown(index, list) {
      console.info("downArrow,", index);
      if (list.length - 1 > index) {
        console.info("upArrow-set,", index, list);
        let curItem = list.splice(index, 1);
        console.info("upArrow-delete,", curItem);
        list.splice(index + 1, 0, ...curItem);
      }
    }
  }
};
</script>
<style lang="scss">
.board {
  width: 1000px;
  margin-left: 20px;
  display: flex;
  justify-content: space-around;
  flex-direction: row;
  align-items: flex-start;
}
.lunbo {
  &.todo {
    .board-column-header {
      background: #4a9ff9;
    }
  }
  &.working {
    .board-column-header {
      background: #f9944a;
    }
  }
  &.done {
    .board-column-header {
      background: #2ac06d;
    }
  }
}
</style>

