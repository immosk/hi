<template>
  <q-page>
    <div class="row">
      
      <!-- <div class="row">
         <div class="q-pa-md">
          <q-btn
            flat
            rounded
            unelevated
            class="bg-primary"
          >
            <div class="q-px-md q-py-sm text-bold text-capitalize text-white">Contact</div>
          </q-btn>
        </div>
      </div> -->
      
      <div class="col text-center">
        <p class="text-bold text-h3 text-uppercase q-mt-md text-primary">
          HI
        </p>

        <p class="text-bold text-h5 text-uppercase q-mt-sm text-primary">
          HIGH INOVATION
        </p>

      </div>
    </div>

    <section>
      <div class="q-ma-md">
        <q-card flat class="bg-secondary rounded-xl">
          <q-card-section>
            <div class="row">
              <div class="col-md-6 col-sm-6 col-xs-12">
                <div class="text-bold text-h4 q-pa-xl">{{ attention }}</div>
                <q-btn @click="onClickAboutUs()" flat rounded unelevated class="bg-primary q-mx-xl q-mb-xl">
                  <div
                    class="q-px-md q-py-sm text-bold text-capitalize text-white">
                    About Us
                  </div>
                </q-btn>
              </div>
              
              <div class="col-md-6 col-sm-6 col-xs-12">
                  <q-img 
                    src="~assets/hello.png"
                  />
              </div>
            </div>
          </q-card-section>
        </q-card>
      </div>
    </section>

    <template v-for="data in dataPortofolio">
      <section :key="data['id']">
          <div class="q-ma-md">
            <q-card flat class="bg-secondary rounded-xl">
              <q-card-section>
                <div class="row">
                  <div class="col-md-6 col-sm-6 col-xs-12">
                    <div class="text-bold text-h3 q-pa-xl text-desc-color">{{ data['name'] }}</div>
                    <div class="text-h5 q-pa-xl">{{ data['desc'] }}</div>
                    
                    <q-btn @click="onClickDetailSection(data['id'])" flat rounded unelevated class="bg-primary q-mx-xl q-mb-xl">
                      <div
                        class="q-px-md q-py-sm text-bold text-capitalize text-white">
                        See Detail
                      </div>
                    </q-btn>
                  </div>
                  
                  <div class="col-md-6 col-sm-6 col-xs-12">
                      <q-img 
                        :src='data["image"]'
                      />
                  </div>
                </div>
              </q-card-section>
            </q-card>
          </div>
      </section>
    </template>
  </q-page>
</template>

<script>
import {
  defineComponent,
  reactive,
  toRefs,
  onMounted,
} from "@vue/composition-api";
import { Notify } from "quasar";

export default defineComponent({
  name: "PageIndex",

  setup() {
    const state = reactive({
      attention: "Get to know us more closely",
      dataPortofolio: [{id: 0, title: '', name: 'HI POS', desc: 'Manage all your bussiness in your hand', image: 'img/hi-pos-disp-dashboard-1.png'}, 
                        {id: 1, title: '', name: 'HI Admin', desc: 'Admin', image: 'img/hi-pos-disp-cashier-1.png'}
                      ],
    });

    onMounted(() => {

    });

    const onClickAboutUs = () => {
    };

    const onClickDetailSection = (id) => {

    }

    return {
      ...toRefs(state),
      onClickAboutUs,
      onClickDetailSection,
    };
  },
});
</script>

<style lang="scss" scoped>
</style>