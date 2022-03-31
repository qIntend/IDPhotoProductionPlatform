<template>
  <section class="section-hero section-shaped my-0">
    <div class="shape shape-style-1 shape-primary">
    </div>
    <div class="myContainer">
      <Canvas />
    </div>
  </section>
</template>
<script>
import Canvas from "./components/Canvas.vue"
export default {
  name: "craft",
  data () {
    return {
      str: 'cnm!!!!!!!!!!!!!!!!!!11111'
    }
  },
  components: {
    Canvas
  },
  methods: {
    handleOpen (key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose (key, keyPath) {
      console.log(key, keyPath);
    }
  }
};
</script>
<style>
.myContainer {
  padding-top: 80px;
}
.text {
  font-size: 14px;
}

.item {
  margin-bottom: 18px;
}

.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}
.clearfix:after {
  clear: both;
}

.box-card {
  width: 300px;
}
</style>