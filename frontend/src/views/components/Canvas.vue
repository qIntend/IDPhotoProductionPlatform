<template>
  <el-container>
    <el-aside>
      <el-form class="handleSave">
        <el-row>
          <base-button
            type="info"
            @click="imgDraw"
            icon="fa fa-plus-square-o"
          >
            <input
              type="file"
              accept="image/*"
              style="display:none"
              id="uploadfile"
              @change="uploadFile"
            />
            上传图片
          </base-button>
          <base-button
            type="warning"
            icon="fa fa-download"
            @click="downLoad"
          >下载图片</base-button>
        </el-row>
        <el-collapse
          v-model="activeNames"
          @change="handleChange"
        >
          <el-collapse-item
            class="ml-2"
            title="证件类型"
            name="1"
          >

          </el-collapse-item>
          <el-collapse-item
            class="ml-2"
            title="换背景"
            name="2"
          >
            <el-row>
              <p style="margin-top:20px; margin-bottom:5px; font-weight: bold">选择背景颜色</p>
              <el-color-picker
                class="color-picker"
                v-model="bgcolor"
                circle
                size="large"
                show-alpha
                :predefine="predefineColors"
                @change="changeBgColor"
                color-format="hex"
              ></el-color-picker>
            </el-row>
          </el-collapse-item>
          <el-collapse-item
            class="ml-2"
            title="智能调色美颜"
            name="3"
          >
            <el-popconfirm title="您确定要美颜吗?有些证件照是不允许美颜的喔~">
              <el-button slot="reference">人像美颜</el-button>
            </el-popconfirm>
          </el-collapse-item>
        </el-collapse>
        <el-row>
          <!-- <el-form-item
            inline="inline"
            class="btn-zoom"
            style="margin: 10px 0px"
          >
            <i
              class="el-icon-caret-left"
              @click="zoomIt(0.8)"
            ></i>
            <span> {{ zoomCounter }} % </span>
            <i
              class="el-icon-caret-right"
              @click="zoomIt(1.2)"
            ></i>
          </el-form-item> -->
          <el-button
            type="danger"
            class="btn-reset"
            @click="resetCanvas"
          >重 置</el-button>
        </el-row>
      </el-form>
    </el-aside>
    <el-main style="height: 715px">
      <div class="content-show">
        <div class="row justify-content-center">
          <canvas
            ref="canvas"
            id="editorCanvas"
          ></canvas>
        </div>
      </div>
    </el-main>
  </el-container>
</template>

<script>
import { fabric } from "fabric";
let editorCanvas = "";

fabric.Object.prototype.set({
  cornerStrokeColor: "#66b0ef",
  cornerColor: "#60abec",
  cornerStyle: "rectangele",
  cornerSize: 8,
  borderScaleFactor: 2,
  transparentCorners: false,
  borderColor: "#61abe8",
});

export default {
  data () {
    return {
      activeNames: ['1'],
      isHide: true,
      checkAll: false,
      isChecked: false,
      isIndeterminate: true,
      backgroundColor,
      predefineColors: ["#ffffff", "#FF0000", "#000000", "#FFF800", "#00FF0A", "#FD00FF", "#0095FF"],
      checked: true,
      // 模板图片保存数组
      templateImgs: [],
      zoomCounter: 100,
      tipTitle: "",
      imageBase64: "",
      isCollapsed: false,
      backColor: "#eec5c5",
      backGroundStatus: false,
      bgcolor: "#ff0000",
      itemWidth: "230px",
      done: false,
      isOpen: false,
      isMove: false,
      src: "",
      msg: "",
      canvas: null,
      templateData: {},
      mouseFrom: {},
      mouseTo: {},
      moveCount: 1,
    };
  },
  mounted () {
    this.initeditorCanvas();
  },
  methods: {
    handleChange (val) {
      console.log(val);
    },
    downLoadImage1 () {
      this.done = true
      let base64URl = editorCanvas.toDataURL({
        formart: 'png',
        multiplier: 1
      })
      this.imageBase64 = base64URl
      this.done = false
    },

    saveTemplates () {
      console.log("你点击了模板保存");
      let base64URl = editorCanvas.toDataURL({
        formart: "jpg",
        multiplier: 1,
      });
    },

    addTemplates () {
      console.log("添加模板");
    },

    initD () {
      // 监听鼠标按下
      const obj = editorCanvas.getActiveObject();
      editorCanvas.on("mouse:down", (options) => {
        // 记录当前鼠标的起点坐标
        if (!obj) {
          this.mouseFrom.x = options.e.clientX - editorCanvas._offset.left;
          this.mouseFrom.y = options.e.clientY - editorCanvas._offset.top;
        }
      });
      // 监听鼠标移动
      editorCanvas.on("mouse:move", (options) => {
        // 记录当前鼠标移动终点坐标
        if (!obj) {
          this.mouseTo.x = options.e.clientX - editorCanvas._offset.left
          this.mouseTo.y = options.e.clientY - editorCanvas._offset.top
          this.drawRect();
        }
      });
      editorCanvas.on("mouse:up", (options) => {
        if (!obj) {
          this.mouseFrom.x = options.e.clientX - editorCanvas._offset.left;
          this.mouseFrom.y = options.e.clientY - editorCanvas._offset.top;
          this.doDrawing = false;
          this.canvasObject = null;
          this.mouseFrom = {};
          this.mouseTo = {}
        }
      });
      editorCanvas.on("selection:created", (option) => {
        if (option) {
          this.doDrawing = false;
        }
      })
    },
    getTransformedPosX (x) {
      let zoom = Number(editorCanvas.getZoom())
      return (x - editorCanvas.viewportTransform[4]) / zoom;
    },
    getTransformedPosY (y) {
      let zoom = Number(editorCanvas.getZoom())
      return (y - editorCanvas.viewportTransform[5]) / zoom;
    },

    // 初始化模板编辑画布
    initeditorCanvas () {
      // 根据不同证件照要求创建框框
      // 创建一个矩形对象
      // TODO 后面改成虚线框出来这样效果肯定更好 再根据选择的类型选择颜色以及方框大小
      let rect = new fabric.Rect({
        left: 450, //距离左边的距离
        top: 100, //距离上边的距离
        fill: "skyblue", //填充的颜色
        width: 358, //矩形宽度
        height: 441, //矩形高度
      });

      editorCanvas = new fabric.Canvas("editorCanvas", {
        devicePixelRatio: true,
        width: "1185",
        height: "650",
        originX: "center",
        originY: "center",
        backgroundColor: "#ffffff",
        transparentCorners: false,
      });
      editorCanvas.preserveObjectStacking = true;
      editorCanvas.add(rect);
    },

    // 载入图片
    imgDraw () {
      document.getElementById("uploadfile").click();
    },

    uploadFile (e) {
      editorCanvas.isDrawingMode = false;
      let file = e.target.files[0];
      let reader = new FileReader();
      reader.onload = (e) => {
        let data = e.target.result;
        fabric.Image.fromURL(data, (img) => {
          editorCanvas.add(img).renderAll();
        });
      };
      reader.readAsDataURL(file);
      e.target.value = "";
    },

    // 下载图片
    downLoad () {
      this.done = true;
      const dataURL = editorCanvas.toDataURL({
        width: 358,
        height: 441,
        left: 450,
        top: 100,
        format: "png",
      });
      const link = document.createElement("a");
      link.download = "图片.png";
      link.href = dataURL;
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    },

    // 清空画布
    resetCanvas () {
      let children = editorCanvas.getObjects();
      if (children.length > 0) {
        editorCanvas.remove(...children);
      }
      editorCanvas.setBackgroundColor("#fff");
    },

    // 缩放
    zoomIt (factor) {
      let zoomCounter = this.zoomCounter;
      let cWidth = editorCanvas.width;
      let cHeight = editorCanvas.height;

      /* 同步缩小 */
      if (factor < 1 && zoomCounter > 0) {
        this.zoomCounter -= 20;
        editorCanvas.setWidth(cWidth * factor);
        editorCanvas.setHeight(cHeight * factor);

        const objects = editorCanvas.getObjects();
        for (let i in objects) {
          let scaleX = objects[i].scaleX;
          let scaleY = objects[i].scaleY;
          let left = objects[i].left;
          let top = objects[i].top;
          let tempScaleX = scaleX * factor;
          let tempScaleY = scaleY * factor;
          let tempLeft = left * factor;
          let tempTop = top * factor;
          objects[i].scaleX = tempScaleX;
          objects[i].scaleY = tempScaleY;
          objects[i].left = tempLeft;
          objects[i].top = tempTop;
          objects[i].setCoords();
          let zoomPoint = new fabric.Point(
            editorCanvas.width / 2,
            editorCanvas.height / 2
          );
          editorCanvas.zoomToPoint(zoomPoint, factor);
          editorCanvas.renderAll();
          editorCanvas.calcOffset();
        }
      }

      /* 同步放大 */
      if (factor > 1 && zoomCounter < 100) {
        this.zoomCounter += 20;
        editorCanvas.setWidth(cWidth * factor);
        editorCanvas.setHeight(cHeight * factor);
        const objects = editorCanvas.getObjects();
        for (let i in objects) {
          let scaleX = objects[i].scaleX;
          let scaleY = objects[i].scaleY;
          let left = objects[i].left;
          let top = objects[i].top;
          let tempScaleX = scaleX * factor;
          let tempScaleY = scaleY * factor;
          let tempLeft = left * factor;
          let tempTop = top * factor;
          objects[i].scaleX = tempScaleX;
          objects[i].scaleY = tempScaleY;
          objects[i].left = tempLeft;
          objects[i].top = tempTop;
          objects[i].setCoords();
        }
        let zoomPoint = new fabric.Point(
          editorCanvas.width / 2,
          editorCanvas.height / 2
        );
        editorCanvas.zoomToPoint(zoomPoint, factor);
        editorCanvas.renderAll();
        editorCanvas.calcOffset();
      } else {
        return;
      }
    },

    // 背景颜色
    changeBgColor (value) {
      let mbgColor = value;
      const obj = editorCanvas;
      if (obj) {
        obj.set({
          backgroundColor: mbgColor,
        });
        editorCanvas.renderAll();
      }
      this.templateData.bgColor = mbgColor;
    }
  }
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}
body {
  font-family: "PingFang SC", "Helvetica Neue", Helvetica, "microsoft yahei",
    arial, STHeiTi, sans-serif;
}

a {
  text-decoration: none;
}

.handleSave {
  padding-top: 20px;
}

.el-aside {
  background-color: white;
  color: #333;
  text-align: center;
}

.el-main {
  background-color: #eeeeee;
  color: #333;
  text-align: center;
  line-height: 160px;
}

.el-main .content-show {
  display: flex;
  flex-direction: column;
  item-align: center;
}

.text-edit h6 {
  height: 40px;
  color: black;
}

.text-edit .el-form {
  margin: 15px;
}

.btn-delete {
  min-height: 36px;
}

.template-content {
  padding: 0px;
  margin: 0px;
}

ton-box:hover {
  color: white;
  opacity: 1;
}

.templateContent {
  width: 100%;
  padding: 0px;
  background-color: #fff;
}

.template-upload {
  width: 256px;
  height: 130px;
  border: 2px solid #adadad;
  margin: 10px auto;
  line-height: 130px;
  text-align: center;
  cursor: pointer;
}

.template-img {
  width: 300px;
  height: 130px;
  margin: 0px auto;
  line-height: 130px;
  text-align: center;
  cursor: pointer;
}

#editorCanvas {
  box-shadow: 0 0 25px #cac6c6;
  width: 100%;
  display: block;
  margin: 10px auto;
  height: 100%;
}

.text-setting {
  text-align: center;
  width: 80px;
  font-size: 18px;
  font-weight: 500;
  margin-right: 170px;
}

.text-edit h4,
.side-right h4,
.show h1 {
  text-align: center;
  font-size: 16px;
  color: #585858;
  font-weight: normal;
  margin: 15px auto;
}

.show h1 {
  text-align: center;
  color: #585858;
  padding: 15px;
  font-weight: bold;
  font-size: 24px;
  margin: 15px auto;
}

.btn-zoom {
  display: inline-block;
  line-height: 1;
  height: 40px;
  width: 104px;
  white-space: nowrap;
  -webkit-appearance: none;
  text-align: center;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  outline: 0;
  margin: 0;
  -webkit-transition: 0.1s;
  transition: 0.1s;
  font-weight: 500;
  font-size: 14px;
  border-radius: 4px;
  color: #fff;
  background-color: #6a60e3;
  border-color: #6a60e3;
}

.btn-download,
.btn-save,
.btn-load,
.btn-reset {
  display: inline-block;
  line-height: 1;
  height: 40px;
  width: 104px;
  white-space: nowrap;
  -webkit-appearance: none;
  text-align: center;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  outline: 0;
  margin: 0;
  -webkit-transition: 0.1s;
  transition: 0.1s;
  font-weight: 500;
  padding: 12px 20px;
  font-size: 14px;
  border-radius: 4px;
  color: #fff;
  background-color: #6a60e3;
  margin: 10px 0px 0px 10px;
  border-color: #6a60e3;
}

.btn-reset {
  height: 40px;
  color: #fff;
  width: 98px;
  background-color: #6a60e3;
  margin: 10px 0px 0px 10px;
  border-color: #6a60e3;
}

.el-form-item {
  margin: 15px auto;
}

.el-form {
  height: 70px;
  line-height: 70px;
}

.el-header {
  height: 60px;
}

.el-form--inline .el-form-item__content {
  margin: 0;
  padding: 0;
  height: 60px;
}

.btn_style {
  display: inline-block;
  height: 40px;
  margin-left: 15px;
  width: 120px;
  line-height: 40px;
  white-space: nowrap;
  -webkit-appearance: none;
  text-align: center;
  font-weight: 500;
  background: none;
  padding: 0px 20px 20px;
  font-size: 14px;
  border-radius: 4px;
  color: #fff;
}
</style>


