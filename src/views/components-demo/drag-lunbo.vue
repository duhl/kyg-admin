<template>
  <div class="components-container board">
    <LunboClone
      :key="1"
      :list="list1"
      :group="group"
      class="lunbo todo"
      header-text="Todo"
    />
    <Lunbo
      :key="2"
      :list="list2"
      :lunbo-list="lunboList"
      :group="group"
      :active="active"
      :sort-up="handleSortUp"
      :sort-down="handleSortDown"
      :on-active="handleActive"
      class="lunbo working"
      header-text="Working"
    />
    <LunboNoDrag
      :key="3"
      :list="list3"
      :group="group"
      :upload-view="uploadView"
      :add-lunbo="handleAddLunbo"
      class="lunbo done"
      header-text="Done"
    />
  </div>
</template>
<script>
import Lunbo from "@/components/Lunbo";
import LunboClone from "@/components/Lunbo/clone";
import LunboNoDrag from "@/components/Lunbo/noDrag";

export default {
  name: "DragLunboDemo",
  components: {
    Lunbo,
    LunboClone,
    LunboNoDrag
  },
  data() {
    return {
      group: "mission",
      list1: [{ name: "轮播图", id: 1, type: "lunbo" }],
      list2: [
        { name: "图片", id: 5, tyle: "template" },
        { name: "文字", id: 6, tyle: "template" }
        /* { name: "文字", id: 7 } */
      ],
      list3: [
        { name: "Mission", id: 8 },
        { name: "Mission", id: 9 },
        { name: "Mission", id: 10 }
      ],
      lunboList: [],
      active: null,
      uploadView: false
    };
  },
  methods: {
    handleSortUp(index, list) {
      if (index) {
        const curItem = list.splice(index, 1);
        list.splice(index - 1, 0, ...curItem);
      }
    },
    handleSortDown(index, list) {
      if (list.length - 1 > index) {
        const curItem = list.splice(index, 1);
        list.splice(index + 1, 0, ...curItem);
      }
    },
    handleActive(index, element) {
      this.active = index;
      if (element.type === "lunbo") {
        this.uploadView = true;
      } else {
        this.uploadView = false;
      }
    },
    handleAddLunbo(item) {
      this.lunboList.push(item);
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
