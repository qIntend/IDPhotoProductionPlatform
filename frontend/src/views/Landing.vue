<template>
  <div>
    <div class="position-relative">
      <!-- shape Hero -->
      <section class="section-shaped my-0">
        <div class="shape shape-style-1 shape-default shape-skew">
          <span></span>
          <span></span>
          <span></span>
          <span></span>
          <span></span>
          <span></span>
          <span></span>
          <span></span>
          <span></span>
        </div>
        <div class="container shape-container d-flex">
          <div class="col px-0">
            <div class="row">
              <div class="col-lg-6">
                <h1 class="display-3  text-white">正式开始制作证件照
                </h1>
                <!-- <div class="btn-wrapper">
                  <base-button
                    tag="a"
                    href="https://demos.creative-tim.com/argon-design-system/docs/components/alerts.html"
                    class="mb-3 mb-sm-0"
                    type="info"
                    icon="fa fa-code"
                  >
                    上传
                  </base-button>
                  <base-button
                    tag="a"
                    href="https://www.creative-tim.com/product/argon-design-system"
                    class="mb-3 mb-sm-0"
                    type="white"
                    icon="ni ni-cloud-download-95"
                  >
                    拍摄
                  </base-button>
                </div> -->
              </div>
            </div>
          </div>
        </div>
      </section>
      <!-- 1st Hero Variation -->
    </div>
    <section class="section section-lg pt-lg-0 mt--200">
      <div class="container">
        <div class="row justify-content-center">
          <div class="col-lg-12">
            <div class="row row-grid">
              <div class="col-lg-4">
                <card
                  class="border-0"
                  hover
                  shadow
                  body-classes="py-5"
                >
                  <icon
                    name="ni ni-check-bold"
                    type="primary"
                    rounded
                    class="mb-4"
                  >
                  </icon>
                  <h6 class="text-primary text-uppercase">身份证件照</h6>
                  <p class="description mt-3">1.近期正面免冠彩色头像，头和脸不得正斜或侧转。
                  <p class="description mt-3">2.二代证的照片裁切规格为358像素（宽）×441像素（高），二代证的证件照尺寸标准是26mm×32mm。</p>
                  <p class="description mt-3">3.着装上要求尽量穿深色有领衣服，不着制式服装。</p>
                  <p class="description mt-3">4.照片背景要求为白色，照片是无边框的。</p>
                  <p class="description mt-3">5.以及在脸颊宽度和头顶距照片上边的尺寸等，也都有对应的规定要求。</p>
                  <div>
                    <badge
                      type="primary"
                      rounded
                    >design</badge>
                    <badge
                      type="primary"
                      rounded
                    >system</badge>
                    <badge
                      type="primary"
                      rounded
                    >creative</badge>
                  </div>
                  <!-- <base-button
                    tag="a"
                    href="#"
                    type="primary"
                    class="mt-4"
                  >
                    制作身份证件照
                  </base-button> -->
                  <base-button
                    block
                    type="primary"
                    class="mt-4"
                    @click="modals.modal1 = true"
                  >
                    制作身份证件照
                  </base-button>
                </card>
                <modal
                  :show.sync="modals.modal1"
                  gradient="primary"
                  modal-classes="modal-danger modal-dialog-centered"
                >
                  <h6
                    slot="header"
                    class="modal-title"
                    id="modal-title-notification"
                  >请选择上传照片的形式</h6>

                  <div class="py-3 text-center">
                    <i class="ni ni-bell-55 ni-3x"></i>
                    <h4 class="heading mt-4">在制作证件照之前，请先阅读以下注意事项！</h4>
                    <p>证件照的要求是免冠（不戴帽子）正面照片，照片上正常应该看到人的两耳轮廓和相当于男士的喉结处的地方。同时，
                      你要穿有领子的衣服，不能化妆化得过浓，影响你的真实面貌，只可以涂淡淡的口红，要见耳朵、见到颈部，头上不戴任何装束。</p>
                  </div>

                  <template slot="footer">
                    <!-- <base-button type="white">Ok, Got it</base-button> -->
                    <div class="btn-wrapper">
                      <base-button
                        tag="a"
                        href="https://demos.creative-tim.com/argon-design-system/docs/components/alerts.html"
                        class="mb-3 mb-sm-0"
                        type="info"
                        icon="fa fa-code"
                      >
                        上传
                      </base-button>
                      <base-button
                        @click="toCameraPage()"
                        class="mb-3 mb-sm-0"
                        type="white"
                        icon="ni ni-cloud-download-95"
                      >
                        拍摄
                      </base-button>
                    </div>
                    <base-button
                      type="link"
                      text-color="white"
                      class="ml-auto"
                      @click="modals.modal1 = false"
                    >
                      Close
                    </base-button>
                  </template>
                </modal>
              </div>
              <div class="col-lg-4">
                <card
                  class="border-0"
                  hover
                  shadow
                  body-classes="py-5"
                >
                  <icon
                    name="ni ni-istanbul"
                    type="success"
                    rounded
                    class="mb-4"
                  >
                  </icon>
                  <h6 class="text-success text-uppercase">护照照片要求</h6>
                  <p class="description mt-3">1.新版护照所需要的照片必须是近期拍摄的直边正面免冠彩色半身证件照片。</p>
                  <p class="description mt-3">2.照片背景颜色为白色或淡蓝色，着白色服装的须用淡蓝色背景，着其他颜色服装使用白色背景。着装上尽量穿着深色有领衣服，公职人员不着制式服装。</p>
                  <p class="description mt-3">3.中国护照的证件照尺寸为48mm×33mm，人像头部宽度21mm－24mm，头部长度28mm－33mm。</p>
                  <p class="description mt-3">4.以及在人像的清晰度等方面都还有一定的要求。</p>
                  <div>
                    <badge
                      type="success"
                      rounded
                    >business</badge>
                    <badge
                      type="success"
                      rounded
                    >vision</badge>
                    <badge
                      type="success"
                      rounded
                    >success</badge>
                  </div>
                  <!-- <base-button
                    tag="a"
                    href="#"
                    type="success"
                    class="mt-4"
                  >
                    开始制作护照证件照
                  </base-button> -->
                  <base-button
                    block
                    type="success"
                    class="mt-4"
                    @click="modals.modal2 = true"
                  >
                    开始制作护照证件照
                  </base-button>
                </card>
                <modal
                  :show.sync="modals.modal2"
                  gradient="success"
                  modal-classes="modal-danger modal-dialog-centered"
                >
                  <h6
                    slot="header"
                    class="modal-title"
                    id="modal-title-notification"
                  >请选择上传照片的形式</h6>

                  <div class="py-3 text-center">
                    <i class="ni ni-bell-55 ni-3x"></i>
                    <h4 class="heading mt-4">在制作证件照之前，请先阅读以下注意事项！</h4>
                    <p>证件照的要求是免冠（不戴帽子）正面照片，照片上正常应该看到人的两耳轮廓和相当于男士的喉结处的地方。同时，
                      你要穿有领子的衣服，不能化妆化得过浓，影响你的真实面貌，只可以涂淡淡的口红，要见耳朵、见到颈部，头上不戴任何装束。</p>
                  </div>

                  <template slot="footer">
                    <!-- <base-button type="white">Ok, Got it</base-button> -->
                    <div class="btn-wrapper">
                      <base-button
                        tag="a"
                        href="https://demos.creative-tim.com/argon-design-system/docs/components/alerts.html"
                        class="mb-3 mb-sm-0"
                        type="info"
                        icon="fa fa-code"
                      >
                        上传
                      </base-button>
                      <base-button
                        tag="a"
                        href="https://www.creative-tim.com/product/argon-design-system"
                        class="mb-3 mb-sm-0"
                        type="white"
                        icon="ni ni-cloud-download-95"
                      >
                        拍摄
                      </base-button>
                    </div>
                    <base-button
                      type="link"
                      text-color="white"
                      class="ml-auto"
                      @click="modals.modal2 = false"
                    >
                      Close
                    </base-button>
                  </template>
                </modal>
              </div>
              <div class="col-lg-4">
                <card
                  class="border-0"
                  hover
                  shadow
                  body-classes="py-5"
                >
                  <icon
                    name="ni ni-planet"
                    type="warning"
                    rounded
                    class="mb-4"
                  >
                  </icon>
                  <h6 class="text-warning text-uppercase">签证证件照要求</h6>
                  <p class="description mt-3">1.申请人的照片必须是无边框的，为最近六个月内所拍摄的正面证件照，要求从照片可以清晰辨别出申请人。</p>
                  <p class="description mt-3">2.国签证的证件照尺寸为2X2英寸 (大约50mmX50mm)正方形，头像居于照片正中。头部(从头顶至下巴)在25mm－35mm，眼睛到照片底部的距离在即28mm－35mm。</p>
                  <p class="description mt-3">3.背景颜色可以是白色或浅色背景的彩色或黑白的无边框照片，美国签证的证件照规格与美国护照的是相同。</p>
                  <p class="description mt-3">4.如果照片不符合新的美国签证的证件照规格标准，非移民签证申请将不被接受。</p>
                  <div>
                    <badge
                      type="warning"
                      rounded
                    >marketing</badge>
                    <badge
                      type="warning"
                      rounded
                    >product</badge>
                    <badge
                      type="warning"
                      rounded
                    >launch</badge>
                  </div>
                  <!-- <base-button
                    tag="a"
                    href="#"
                    type="warning"
                    class="mt-4"
                  >
                    开始制作签证证件照
                  </base-button> -->
                  <base-button
                    block
                    type="warning"
                    class="mt-4"
                    @click="modals.modal3 = true"
                  >
                    开始制作签证证件照
                  </base-button>
                </card>
                <modal
                  :show.sync="modals.modal3"
                  gradient="danger"
                  modal-classes="modal-danger modal-dialog-centered"
                >
                  <h6
                    slot="header"
                    class="modal-title"
                    id="modal-title-notification"
                  >请选择上传照片的形式</h6>

                  <div class="py-3 text-center">
                    <i class="ni ni-bell-55 ni-3x"></i>
                    <h4 class="heading mt-4">在制作证件照之前，请先阅读以下注意事项！</h4>
                    <p>证件照的要求是免冠（不戴帽子）正面照片，照片上正常应该看到人的两耳轮廓和相当于男士的喉结处的地方。同时，
                      你要穿有领子的衣服，不能化妆化得过浓，影响你的真实面貌，只可以涂淡淡的口红，要见耳朵、见到颈部，头上不戴任何装束。</p>
                  </div>

                  <template slot="footer">
                    <!-- <base-button type="white">Ok, Got it</base-button> -->
                    <div class="btn-wrapper">
                      <base-button
                        tag="a"
                        href="https://demos.creative-tim.com/argon-design-system/docs/components/alerts.html"
                        class="mb-3 mb-sm-0"
                        type="info"
                        icon="fa fa-code"
                      >
                        上传
                      </base-button>
                      <base-button
                        tag="a"
                        href="https://www.creative-tim.com/product/argon-design-system"
                        class="mb-3 mb-sm-0"
                        type="white"
                        icon="ni ni-cloud-download-95"
                      >
                        拍摄
                      </base-button>
                    </div>
                    <base-button
                      type="link"
                      text-color="white"
                      class="ml-auto"
                      @click="modals.modal3 = false"
                    >
                      Close
                    </base-button>
                  </template>
                </modal>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Modal from "@/components/Modal.vue"
export default {
  name: "home",
  components: {
    Modal
  },
  data () {
    return {
      modals: {
        modal1: false,
        modal2: false,
        modal3: false
      }
    };
  },
  methods: {
    toCameraPage () {
      this.$router.push('/camera');
    }
  }
};
</script>

<style lang="scss" scoped>
</style>
