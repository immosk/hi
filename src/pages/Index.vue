<template>
  <q-page>
    <div class="row">
      <div class="col text-center">
        <p class="text-bold text-h5 text-uppercase q-mt-md text-harris">
          Welcome back!
        </p>
      </div>
    </div>

    <section>
      <div class="q-ma-md">
        <q-card flat class="bg-cyan-1 rounded-xl">
          <q-card-section>
            <div class="row">
              <div class="col-md-6 col-sm-6 col-xs-12">
                <div class="text-bold text-h4 q-pa-xl">{{ attention }}</div>
                <q-btn @click="onClickNugget" flat rounded unelevated class="bg-primary q-mx-xl q-mb-xl">
                  <div
                    class="q-px-md q-py-sm text-bold text-capitalize text-white"
                  >
                    We have digitalized
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
      attention: "Create a Digital Business with Primy to get more attention",
    });

    onMounted(() => {
       Notify.create({
        type: "info",
        message: "Composition api is ready!",
      });
    });

    const onClickNugget = () => {
      Notify.create({
        type: "info",
        message: "Quantity cannot be 0",
      });
    };

    return {
      ...toRefs(state),
      onClickNugget,
    };
  },
});
</script>

<style lang="scss" scoped>
</style>