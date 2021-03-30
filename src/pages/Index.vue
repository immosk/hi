<template>
  <q-page>
    <div class="row">
      <div class="col text-center">
        <p class="text-bold text-h3 text-uppercase q-mt-md text-primary">
          HI
        </p>

        <!-- <p class="text-bold text-h5 text-uppercase q-mt-sm text-primary">
          HIGH INOVATION
        </p> -->

      </div>
    </div>

    <section>
      <div class="q-ma-md">
        <q-card flat class="section-intro-bg-primary rounded-xl">
          <q-card-section>
            <div class="row">
              <div class="col-md-6 col-sm-6 col-xs-12">
                <div class="text-bold text-h4 q-pa-xl">{{ attention }}</div>
                <q-btn @click="onClickAboutUs()" flat rounded unelevated class="bg-primary q-mx-xl q-mb-xl">
                  <div
                    class="q-px-md q-py-sm text-bold text-capitalize text-white">
                    Portofolio
                  </div>
                </q-btn>
              </div>
              
              <!-- <div class="col-md-6 col-sm-6 col-xs-12">
                  <q-img 
                    src="~assets/hello.png"
                  />
              </div> -->
            </div>
          </q-card-section>
        </q-card>
      </div>
    </section>

    <template v-for="data in dataPortofolio">
      <section id="portofolio" :key="data['id']">
          <div class="q-ma-md">
            <q-card flat class="bg-secondary rounded-xl" >
              <div class="col text-center">
                <p class="text-bold text-h5 text-uppercase q-mt-md text-primary">
                </p>
              </div>

              <q-card-section>
                <div class="row">
                  <div class="col-md-6 col-sm-6 col-xs-12">
                    <div class="text-bold text-h3 q-pa-xl text-desc-color">{{ data['name'] }}</div>
                    <div class="text-h4 q-px-xl q-py-md">{{ data['desc'] }}</div>

                    <template v-for="dataDesc in data['imagedata']">
                      <div 
                        :key="dataDesc['id']" 
                        class="text-h5 q-px-xl q-pb-md">
                          <div v-if="dataDesc['id'] == slide">
                            {{ dataDesc['desc']}}
                          </div>
                        </div>
                    </template>
                    <!-- <div class="text-h5 q-px-xl q-pb-md">{{ slide == 1 ? data['imagedata'][0]['desc']: slide == 2 ? data['imagedata'][1]['desc'] : slide == 3 ? data['imagedata'][2]['desc'] : data['imagedata'][3]['desc'] }}</div> -->
                    
                    <q-btn @click="onClickDetailSection(data['id'])" flat rounded unelevated class="bg-primary q-mx-xl q-mb-xl">
                      <div
                        class="q-px-md q-py-sm text-bold text-capitalize text-white">
                        See Detail
                      </div>
                    </q-btn>
                  </div>
                  
                  <div class="col-md-6 col-sm-6 col-xs-12">
                      <q-carousel
                        v-model="slide"
                        animated
                        arrows
                        swipeable
                        infinite
                        autoplay>
                        <template v-for="dataimage in data['imagedata']"> 
                          <q-carousel-slide :key="dataimage['id']" :name="dataimage['id']" :img-src="(dataimage['image'])" />
                        </template>
                      </q-carousel>
                      
                      <!-- <q-img 
                        :src="(data['imagedata'][0]['image'])"
                      /> -->
                  </div>
                </div>
              </q-card-section>
            </q-card>
          </div>
      </section>
    </template>

    <section id="footer">
      <q-card flat class="q-mx-sm q-mt-sm bg-primary">
        <q-card-section>

          <div class="row justify-center">
            <div class="col-12 col-md-auto">
              <q-img class="q-ma-sm" src="~assets/ic-linkedin.png" width="40px" height="40px"/>
            </div>

            <div class="col-12 col-md-auto">
              <q-img class="q-ma-sm" src="~assets/ic-email.png" width="40px" height="40px"/>
            </div>

            <div class="col-12 col-md-auto">
              <q-img class="q-ma-sm" src="~assets/ic-wa.png" width="40px" height="40px"/>
            </div>

          </div>
        </q-card-section>

        <dialogDetail :showDialogDetail="showDialogDetail" @onDialogDetail="onDialogDetail"/>

      </q-card>
    </section>
  </q-page>
</template>

<script>
import { defineComponent, reactive, toRefs, onMounted, } from "@vue/composition-api";
import { Notify } from "quasar";
import DetailPortofolio from "../components/DetailPortofolio.vue";

export default defineComponent({
  name: "PageIndex",

  setup(props, {$root}) {
    const state = reactive({
      attention: "Get to know us more closely",
      dataPortofolio: [{id: 0, title: 'HI POS', name: 'Point Of Sales', desc: 'Manage all your business needs in your hand', imagedata: [{id: 1, desc: 'Realtime Dashboard, see how your outlet grow', image: 'assets/hi-pos-disp-dashboard-1.png'}, {id: 2, desc: 'Add an item and ready to sale ', image: 'assets/hi-pos-disp-edit-lib-1.png'}, {id: 3, desc: 'Cashier with best experience', image:'assets/hi-pos-disp-cashier-1.png'}, {id: 4, desc: 'Don\'t worry about your preferences, it\'s on the cloud!', image: 'assets/hi-pos-disp-pref-1.png'}], cssdata : {'bg-color-primary': 'section-1-bg-primary', 'bg-color-secondary':'section-1-bg-secondary', 'text-color-primary': 'section-1-text-primary', 'text-color-secondary': 'section-1-text-secondary'}}, 
                        // {id: 1, title: 'HI Admin', name: 'General Administration System', desc: 'Admin', imagedata: [{desc: 'Realtime Dashboard, see how your outlet grow', image: 'assets/hi-pos-disp-dashboard-1.png'}], cssdata : {'bg-color-primary': 'section-1-bg-primary', 'bg-color-secondary':'section-1-bg-secondary', 'text-color-primary': 'section-1-text-primary', 'text-color-secondary': 'section-1-text-secondary'}}
                      ],
      slide: 1,
      showDialogDetail: false,
    });

    onMounted(() => {

    });

    const onClickAboutUs = () => {
      const el = document.getElementById('portofolio');
      if (el) {
        el.scrollIntoView({behavior: 'smooth'});
      }
    };

    const onClickDetailSection = (id) => {
      state.showDialogDetail = true;
    }

    const onDialogDetail = (val) => {
      state.showDialogDetail = val;
    }

    return {
      ...toRefs(state),
      onClickAboutUs,
      onClickDetailSection,
      onDialogDetail,
    };
  },
  components: {
    dialogDetail: () => import('../components/DetailPortofolio.vue')
  }
});
</script>

<style lang="scss" scoped>
</style>