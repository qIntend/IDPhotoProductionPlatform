<template>
  <div class="row justify-content-center">
    <div class="col-lg-16">
      <tabs
        fill
        class="flex-column flex-md-row"
      >
        <card
          shadow
          slot-scope="{activeTabIndex}"
        >
          <tab-pane key="tab1">
            <template slot="title">
              <i class="fa fa-id-card-o mr-2"></i>证件照
            </template>
            <Images></Images>
          </tab-pane>

          <tab-pane key="tab2">
            <template slot="title">
              <i class="fa fa-coffee mr-2"></i>职业照
            </template>

            <p class="description">Cosby sweater eu banh mi, qui irure terry richardson ex
              squid. Aliquip placeat salvia cillum iphone. Seitan aliquip quis cardigan
              american apparel, butcher voluptate nisi qui.</p>
          </tab-pane>

          <tab-pane key="tab3">
            <template slot="title">
              <i class="fa fa-camera-retro mr-2"></i>形象照（半身）
            </template>

            <p class="description">Raw denim you probably haven't heard of them jean shorts
              Austin. Nesciunt tofu stumptown aliqua, retro synth master cleanse. Mustache
              cliche tempor, williamsburg carles vegan helvetica. Reprehenderit butcher retro
              keffiyeh dreamcatcher synth.</p>
          </tab-pane>

          <tab-pane key="tab4">
            <template slot="title">
              <i class="fa fa-camera-retro mr-2"></i>形象照（全身）
            </template>

            <p class="description">Raw denim you probably haven't heard of them jean shorts
              Austin. Nesciunt tofu stumptown aliqua, retro synth master cleanse. Mustache
              cliche tempor, williamsburg carles vegan helvetica. Reprehenderit butcher retro
              keffiyeh dreamcatcher synth.</p>
          </tab-pane>

          <tab-pane key="tab5">
            <template slot="title">
              <i class="fa fa-graduation-cap mr-2"></i>入学照
            </template>

            <p class="description">Raw denim you probably haven't heard of them jean shorts
              Austin. Nesciunt tofu stumptown aliqua, retro synth master cleanse. Mustache
              cliche tempor, williamsburg carles vegan helvetica. Reprehenderit butcher retro
              keffiyeh dreamcatcher synth.</p>
          </tab-pane>

          <tab-pane key="tab6">
            <template slot="title">
              <i class="fa fa-paw mr-2"></i>宠物照
            </template>

            <p class="description">Raw denim you probably haven't heard of them jean shorts
              Austin. Nesciunt tofu stumptown aliqua, retro synth master cleanse. Mustache
              cliche tempor, williamsburg carles vegan helvetica. Reprehenderit butcher retro
              keffiyeh dreamcatcher synth.</p>
          </tab-pane>
        </card>
      </tabs>
    </div>
    <!-- <div class="col-lg-6 mt-5 mt-lg-0">
            <div class="mb-3">
                <small class="text-uppercase font-weight-bold">With text</small>
            </div>
            <tabs fill class="flex-column flex-md-row">
                <card shadow>
                    <tab-pane title="Home">
                        <p class="description">Raw denim you probably haven't heard of them jean shorts
                            Austin. Nesciunt tofu stumptown aliqua, retro synth master cleanse. Mustache
                            cliche tempor, williamsburg carles vegan helvetica. Reprehenderit butcher retro
                            keffiyeh dreamcatcher synth.</p>
                        <p class="description">Raw denim you probably haven't heard of them jean shorts
                            Austin. Nesciunt tofu stumptown aliqua, retro synth master cleanse.</p>
                    </tab-pane>

                    <tab-pane title="Profile">
                        <p class="description">Cosby sweater eu banh mi, qui irure terry richardson ex
                            squid. Aliquip placeat salvia cillum iphone. Seitan aliquip quis cardigan
                            american apparel, butcher voluptate nisi qui.</p>
                    </tab-pane>

                    <tab-pane title="Messages">
                        <p class="description">Raw denim you probably haven't heard of them jean shorts
                            Austin. Nesciunt tofu stumptown aliqua, retro synth master cleanse. Mustache
                            cliche tempor, williamsburg carles vegan helvetica. Reprehenderit butcher retro
                            keffiyeh dreamcatcher synth.</p>
                    </tab-pane>
                </card>
            </tabs>
        </div> -->
  </div>
</template>
<script>
import Tabs from "@/components/Tabs/Tabs.vue";
import TabPane from "@/components/Tabs/TabPane.vue";
import Images from "./Images.vue"
export default {
  components: {
    Tabs,
    TabPane,
    Images
  }
};
</script>
<style>
</style>
