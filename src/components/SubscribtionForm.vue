<template>
  <div class="q-pa-md q-gutter-sm">
    <q-dialog
      v-model="dialogModel"
      persistent
      transition-show="slide-up"
      transition-hide="slide-down">
      <q-card 
        class="bg-white text-primary"
        style="max-width: 650px; min-width: 650px;">
        <q-bar class="q-pa-lg">
          <div class="text-bold text-h5">SUBSCRIPTION</div>

          <q-space />
        </q-bar>

        <template v-if="isPlanOk">
          <q-card-section class="q-pt-none scroll" style="max-height: 70vh">
            <div class="q-ma-sm">
              <q-card flat>
                <q-card-section>
                    <q-input v-model="formData.email" label="Email" />
                    <q-input v-model="formData.name" label="Name" />
                    <q-input v-model="formData.bussinessName" label="Bussiness Name" />
                    <q-input v-model="formData.license" label="Trial License" />
                </q-card-section>
              </q-card>
            </div>
          </q-card-section>
        </template>

        <template v-else>
          <q-card-section class="q-pt-none scroll" style="max-height: 70vh">
            <div class="q-ma-sm">
              <q-card flat>
                <q-card-section>
                  <div class="row-md-6 col-sm-6 col-xs-12">
                    <div class="col q-pb-md"> 

                      <div class="text-bold text-h6 q-pa-mx">Within Subscription you get : </div>
                      
                      <div class="q-px-md q-pt-md text-accent">• Remove your Trial License </div>
                      <div class="q-px-md q-pt-md text-accent">• Add more Outlet (up to 5 Outlet) </div>
                      <div class="q-px-md q-pt-md text-accent">• Add more Employee (up to 30 Employee) </div>
                      <div class="q-px-md q-pt-md text-accent">• Add more Article (up to 50 Article) </div>
                    </div>
                  </div>


                  <div class="col-md-6 col-sm-6 col-xs-12">
                    <div class="row q-pb-md"> 
                        <div class="text-bold text-h6 q-pa-mx">Need extra slot? Choose a plan that suits with yours</div>
                        <q-icon class="q-pa-mx q-my-sm q-mx-sm" name="help">
                          <q-tooltip content-class="bg-primary text-white"> Contact us for more Information </q-tooltip>
                        </q-icon> 
                      </div>
                    </div>

                    <q-chip color="primary" text-color="white">
                      Outlet : Rp.{{formatterMoney(planData.outlet * 1000)}} for extra {{ planData.outlet }} Outlet
                    </q-chip>

                    <q-slider
                      v-model="planData.outlet"
                      markers
                      :min="0"
                      :max="30"
                      :step="10"
                      label
                      :label-value="planData.outlet" 
                      color="accent"
                      @change="onChangeSlider('outlet')"/>

                    <q-chip color="primary" text-color="white">
                      Employee : Rp.{{formatterMoney(planData.employee * 100)}} for extra {{ planData.employee }} Employee
                    </q-chip>

                    <q-slider
                      v-model="planData.employee"
                      markers
                      :min="0"
                      :max="500"
                      :step="100"
                      label
                      :label-value="planData.employee"
                      color="accent"
                      @change="onChangeSlider('employee')" />

                    <q-chip color="primary" text-color="white">
                      Article : Rp.{{formatterMoney(planData.article * 100)}} for extra {{ planData.article }} Article
                    </q-chip>

                    <q-slider
                      v-model="planData.article"
                      markers
                      :min="0"
                      :max="500"
                      :step="100"
                      label
                      :label-value="planData.article"
                      color="accent"
                      @change="onChangeSlider('article')" />
                  </q-card-section>

                  <div class="row q-pb-md"> 
                    <q-checkbox v-model="planData.incTableManagement" label="Include Table Management" :disable="true" />
                    <q-icon class="q-pa-mx q-my-sm q-mx-sm" name="help">
                      <q-tooltip content-class="bg-primary text-white"> Coming Soon </q-tooltip>
                    </q-icon> 
                  </div>

                  <div class="row q-pb-md"> 
                    <q-checkbox v-model="planData.incEwalletPayment" label="Include E-Wallet Payment" :disable="true" readonly />
                    <q-icon class="q-pa-mx q-my-sm q-mx-sm" name="help">
                      <q-tooltip content-class="bg-primary text-white"> Coming Soon </q-tooltip>
                    </q-icon> 
                  </div>

                </q-card>
              </div>
          </q-card-section>          
        </template>

        <q-card-actions align="right">
          <template v-if="!isPlanOk">
            <q-chip class="q-mx-md" color="primary" text-color="white">
              Total : Rp.{{formatterMoney(dataBalance.balance)}} / Monthly         
            </q-chip>
          </template>

          <q-btn outline color="primary" :label="isPlanOk ? 'Back' : 'Cancel' " @click="onClickAction(false, isPlanOk)"  />
          <q-btn color="primary" :label="isPlanOk ? 'Subscribe' : 'Continue' " @click="onClickAction(true, isPlanOk)" />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </div>
</template>

<script lang="ts">
import { defineComponent, watch, computed, toRefs, reactive } from "@vue/composition-api";
import { Notify } from "quasar";
import ky from 'ky';
import { formatterMoney } from './utils/formatterMoney.utils.js';


export default defineComponent({
  props: {
    showDialogSubscibtion: {type: Boolean, required: true },
  }, 
  setup(props, {emit}) {
    const state = reactive({
      isPlanOk: false,
      dataBalance: {
        balance: 50000,
        outlet: 0,
        employee: 0,
        article: 0,
      },
      formData: {
        email: '',
        name: '',
        bussinessName: '',
        license: '',
      },
      planData : {
        outlet: 0,
        employee: 0,
        article: 0,
        incTableManagement: null,
        incEwalletPayment: null
      }
    });

    watch(() => props.showDialogSubscibtion, (showDialogSubscibtion) => {
      if (props.showDialogSubscibtion) {
        // On Mounted ...
      }
    });

    const dialogModel = computed({
      get: () => props.showDialogSubscibtion,
      set: (val) => {
        emit('onDialogSubscribtion', val);
      },
    });

    const onChangeSlider = (slider) => {
      state.dataBalance.balance = 0;

      if (slider === 'outlet') {
        state.dataBalance.outlet = (state.planData.outlet * 1000);
      } else if (slider === 'employee') {
        state.dataBalance.employee = (state.planData.employee * 100);        
      } else if (slider === 'article') {
        state.dataBalance.article = (state.planData.article * 100);
      }
      state.dataBalance.balance = (state.dataBalance.outlet + state.dataBalance.employee + state.dataBalance.article) + 50000;
    }

    const onClickAction = (isOkButton, isPlanOk) => {
      if (isOkButton) {
        if (isPlanOk) {
          if (state.formData.email.trim() === '') {
            Notify.create({
              message: 'Email cannot be blank',
              type: 'error'                
            })
          } else if (state.formData.name.trim() === '') {
            Notify.create({
              message: 'Name cannot be blank',
              type: 'error'                
            })
          } else if (state.formData.bussinessName.trim() === '') {
            Notify.create({
              message: 'Bussiness Name cannot be blank',
              type: 'error'                
            })
          } else if ( state.formData.license.trim() === '') {
            Notify.create({
              message: 'Trial License cannot be blank',
              type: 'error'                
            })
          } else {
            if (validateEmail(state.formData.email)) {
              getSubcribtion();
            } else {
              Notify.create({
                message: 'Please input correct email',
                type: 'error'                
              })
            }
          }
        } else {
          state.isPlanOk = !state.isPlanOk;
        }
      } else {
        if (isPlanOk) {
          state.isPlanOk = !state.isPlanOk;
        } else {
          state.formData.email = '';
          state.formData.name = '';
          state.formData.bussinessName = '';
          state.formData.license = '';
  
          emit('onDialogSubscribtion', false);        
        }
      }
    }

    const getSubcribtion = () => {
      async function asyncCall() {
        const response = await ky('http://localhost/api/get_user_subcribtion.php', {
          method: 'GET',
          headers: {
            'content-type': 'application/json',
            'dbname': 'hi_main_db_tes',
            'email': state.formData.email,
            'license': state.formData.license,
            'name': state.formData.name,
            'bussiness': state.formData.bussinessName,
          }
        }).json();

        if (response) {
          const msgStr = response['msgstr'];
          const resultok = response['resultok'];

          if (msgStr != '') {
            Notify.create({
              message: msgStr,
              type: 'error'                
            })
          } else {
            if (!resultok) {
              Notify.create({
                message: msgStr,
                type: 'error'                
              })
              return false;
            } else {
              emit('onDialogSubscribtion', false);        
            }
          }

          console.log('response : ', response);

        }

      }
      asyncCall();
    }

    function validateEmail(email) {
      const re = /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    }

    return {
      ...toRefs(state),
      dialogModel,
      onClickAction,
      getSubcribtion,
      onChangeSlider,
      formatterMoney,
    }
  },
  components: {

  }
    
})
</script>