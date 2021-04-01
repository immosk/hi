<template>
  <div class="q-pa-md q-gutter-sm">
    <q-dialog
      v-model="dialogModel"
      persistent
      transition-show="slide-up"
      transition-hide="slide-down">

      <q-card 
        class="bg-primary text-white"
        style="max-width: 1500px; min-width: 1100px;">
        <q-bar class="q-pa-lg">
          <div class="text-bold text-h5">HI POS</div>

          <q-space />

          <q-btn dense flat icon="close" v-close-popup>
            <q-tooltip content-class="bg-white text-primary">Close</q-tooltip>
          </q-btn>
        </q-bar>

        <!-- <q-card-section>
          <div class="text-h6">HI POS</div>
        </q-card-section> -->

        <q-card-section class="q-pt-none scroll" style="max-height: 70vh">
          <div class="q-ma-sm">
            <q-card flat class="detail-section-1-bg-primary rounded-xl">
              <q-card-section>
                <div class="row">
                  <div class="col-md-6 col-sm-6 col-xs-12">
                    <div class="row"> 
                      <div class="text-bold text-h5 q-pa-mx">Features</div> 
                      <q-icon class="q-pa-mx q-my-sm q-mx-sm" name="help">
                        <q-tooltip content-class="bg-white text-primary">* Base on your subscription </q-tooltip>
                      </q-icon> 
                    </div>

                    <div class="q-px-md q-pt-md">• Cloud base </div>
                    <div class="q-px-md">• Manage multiple Outlet * </div>
                    <div class="q-px-md">• Multiple bussiness in one system </div>
                    <div class="q-px-md">• Get Revenue, Article Stock, Sales and many more within Aurora's Dashboard </div>
                    <div class="q-px-md">• Manage your team role in Employee tab section * </div>
                    <div class="q-px-md">• Add category and article * </div>
                    <div class="q-px-md">• Add your valueable customer and keep in touch </div>
                    <div class="q-px-md">• Of course it is, Reporting!! No more need to collect receipts papper *  </div>
                    <div class="q-px-md">• All your preferences inside your tablet </div>

                  </div>
                  
                  <div class="col-md-6 col-sm-6 col-xs-12">
                      <q-img 
                        src="../../public/assets/hi-pos-disp-cashier-1.png"
                      />
                  </div>
                </div>
              </q-card-section>
            </q-card>
          </div>

          <div class="q-ma-sm">
            <q-card flat class="detail-section-1-bg-primary rounded-xl">
              <q-card-section>
                <div class="row">
                  <div class="col-md-6 col-sm-6 col-xs-12">
                    <div class="text-bold text-h5 q-pa-mx">Connect to your Mini Bluetooth Printer</div>

                    <div class="q-px-md q-pt-md">• Print all recipe to your customer. Don't want use a paper? We send it to your customer email </div>

                  </div>
                  
                  <div class="col-md-6 col-sm-6 col-xs-12">
                      <q-img 
                        src="../../public/assets/printer.png"
                        height="300px"
                        width="300px"
                      />
                  </div>
                </div>
              </q-card-section>
            </q-card>
          </div>

          <div class="q-ma-sm">
            <q-card flat class="detail-section-1-bg-primary rounded-xl">
              <q-card-section>
                <div class="row">
                  <div class="col-md-6 col-sm-6 col-xs-12">
                    <div class="row"> 
                      <div class="text-bold text-h5 q-pa-mx">Connect to your Bluetooth Scanner</div>
                        <q-icon class="q-pa-mx q-my-sm q-mx-sm" name="help">
                          <q-tooltip content-class="bg-white text-primary">Only support 1D scanner (EAN or UPC) </q-tooltip>
                        </q-icon> 
                      </div>

                    <div class="q-px-md q-pt-md">• Scan barcode item with easy configuration  </div>
                  </div>
                  
                  <div class="col-md-6 col-sm-6 col-xs-12">
                      <q-img 
                        src="../../public/assets/scanner.png"
                        height="300px"
                        width="300px" />
                  </div>
                </div>
              </q-card-section>
            </q-card>
          </div>

          <div class="q-ma-sm">
            <div class="row">
              <div>
                <q-btn type="a" href="https://play.google.com/store/apps" target="_blank" flat rounded unelevated class="bg-white q-mx-xl q-mb-xl">
                  <div class="q-px-md q-py-sm text-bold text-capitalize text-primary">
                    Download
                  </div>
                </q-btn>

                 <q-btn @click="onClickSubcribtion()" flat rounded unelevated class="bg-white q-mx-xl q-mb-xl">
                  <div class="q-px-md q-py-sm text-bold text-capitalize text-primary">
                    Subscription Only Rp.50K / month
                  </div>
                </q-btn>
              </div>                  
            </div>
          </div>

          <dialogSubscription 
            :showDialogSubscibtion="showDialogSubscibtion"
            @onDialogSubscribtion="onDialogSubscribtion"/>

        </q-card-section>
      </q-card>
    </q-dialog>
  </div>
</template>

<script lang="ts">
import { defineComponent, watch, computed, toRefs, reactive } from "@vue/composition-api";


export default defineComponent({
  props: {
    showDialogDetail: {type: Boolean, required: true },
  }, 
  setup(props, {emit}) {

    const state = reactive({
      showDialogSubscibtion: false,
    });

    watch(() => props.showDialogDetail, (showDialogDetail) => {
      if (props.showDialogDetail) {

      }
    });

    const dialogModel = computed({
      get: () => props.showDialogDetail,
      set: (val) => {
        emit('onDialogDetail', val);
      },
    });

    const onClickSubcribtion = () => {
      state.showDialogSubscibtion = true;
    }

    const onDialogSubscribtion = (val) => {
      state.showDialogSubscibtion = val;
    }

    return {
      ...toRefs(state),
      dialogModel,
      onDialogSubscribtion,
      onClickSubcribtion,
    }
  },
  components: {
    dialogSubscription: () => import('./SubscribtionForm.vue')
  }
    
})
</script>