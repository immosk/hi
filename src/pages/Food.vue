<template>
  <q-page>
    <div class="q-pa-md">
      <p class="text-h5 text-bold text-uppercase text-harris">
        Harris <br />
        Restaurant
      </p>
      <p class="q-mb-md">Good Morning, <span class="text-bold"> BALA</span></p>
      <span class="text-uppercase text-bold text-h6 text-harris">Food </span>
      <span class="text-uppercase text-bold text-h6">Menu</span>

      <section>
        <div class="row items-start q-gutter-md">
          <q-card class="my-card" flat bordered>
            <q-card-section horizontal>
              <q-card-section>
                <p class="text-bold text-uppercase">{{ title }}</p>
                <p>{{ notes }}</p>
                <div class="row q-mt-md items-center">
                  <div class="col-6">
                    <div class="text-harris">
                      <span class="text-xs">Rp </span>
                      <span class="text-bold">43,000</span>
                    </div>
                  </div>
                  <div class="col-6 text-right">
                    <q-btn
                      flat
                      dense
                      round
                      color="red-10"
                      size="sm"
                      icon="remove_circle"
                      @click="onClickMinus"
                      v-model="minus"
                    />
                    <span>{{ angka }}</span>
                    <q-btn
                      flat
                      dense
                      round
                      color="primary"
                      size="sm"
                      icon="add_circle"
                      @click="onClickPlus"
                      v-model="showMinus"
                    />
                  </div>
                </div>
              </q-card-section>

              <q-img
                @click="onClickDetailFood"
                class="col-3 cover"
                src="~assets/food_1.png"
              />
            </q-card-section>
          </q-card>
        </div>
      </section>

      <q-btn
        class="q-mt-xl"
        color="primary"
        text-color="white"
        unelevated
        to="/"
        label="Go Home"
        no-caps
      />
    </div>
  </q-page>
</template>

<script>
import {
  defineComponent,
  reactive,
  toRefs,
  onMounted,
} from "@vue/composition-api";
import data from "../../data/data.json";
import { useRouter, useRoute } from "vue-router";

export default defineComponent({
  name: "PageFood",

  setup({ root }) {
    //   const router = useRouter()

    const state = reactive({
      title: "Egg And Cheese Muffin",
      notes: "Perpaduan scrambled edd dan keju gurih dalam setangkup muffin",
      showMinus: false,
      angka: 0,
      minus: false,
      data: {},
    });

    onMounted(() => {
      console.log(data);
    });

    const onClickPlus = () => {
      state.angka++;
      if (state.angka == 0) {
        console.log("Nol ilang: ");
        // state.minus = ``
      }
    };

    const onClickMinus = () => {
      state.angka--;
    };

    const onClickDetailFood = () => {
    //   root.router.push({ path: "" });
      alert('Router to detail food');
    };

    return {
      ...toRefs(state),
      onClickPlus,
      onClickMinus,
      onClickDetailFood,
    };
  },
});
</script>

<style lang="scss" scoped>
.my-card {
  width: 100%;
  //   max-width: 350px;
}

.cover {
  object-fit: contain;
}
</style>