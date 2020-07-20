<template>
  <div class="board-column">
    <div class="board-column-header">
      {{ headerText }}
    </div>
    <div v-if="uploadView" class="upload">
      <el-upload
        class="upload-demo"
        action="/shop/Upload/upload_oss"
        :on-success="handleSuccess"
        :file-list="fileList"
        list-type="picture"
      >
        <el-button size="small" type="primary">点击上传</el-button>
        <div slot="tip" class="el-upload__tip">
          只能上传jpg/png文件，且不超过500kb
        </div>
      </el-upload>
    </div>
  </div>
</template>

<script>
// import draggable from "vuedraggable";
// import axios from 'axios'

export default {
  name: "DragLunboDemo",
  components: {
    // draggable
  },
  props: {
    headerText: {
      type: String,
      default: "Header"
    },
    uploadView: {
      type: Boolean,
      default: false
    },
    addLunbo: {
      type: Function,
      default() {
        return () => {};
      }
    }
  },
  data() {
    return {
      /* active: null, */
      fileList: [
        /* {
          name: "food.jpeg",
          url:
            "https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100"
        },
         */
      ]
    };
  },
  methods: {
    setData(dataTransfer) {
      console.info("dataTransfer", dataTransfer);
      // to avoid Firefox bug
      // Detail see : https://github.com/RubaXa/Sortable/issues/1012
      dataTransfer.setData("Text", "");
    },
    handleSuccess(response) {
      console.log(response);
      this.addLunbo({ images: response.data });
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
      height: 64px;
      margin: 5px 0;
      background-color: #fff;
      text-align: left;
      line-height: 54px;
      padding: 5px 10px;
      box-sizing: border-box;
      box-shadow: 0px 1px 3px 0 rgba(0, 0, 0, 0.2);
      .icon {
        width: 18px;
        height: 100%;
        // border: 1px solid red;
        float: right;
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
      border: 1px solid red;
    }
  }
}
</style>
