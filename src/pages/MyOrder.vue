<template>
  <q-page>
    <div class="q-pa-md">
      <p class="text-h5 q-mb-md text-bold text-uppercase text-harris">
        My <br />
        Order
      </p>

      <section>
        <q-card flat bordered>
          <q-card-section>
            <div class="text-h6">No. #1</div>
            <div class="row">
              <div class="col">
                <div class="row">
                  <div class="col-5 text-uppercase">Name:</div>
                  <div class="col-5 text-uppercase text-harris text-bold">
                    Bala
                  </div>
                  <div class="col-5 text-uppercase">Table:</div>
                  <div class="col-5 text-uppercase">10</div>
                </div>
              </div>
              <div class="col">
                <div class="text-harris text-right text-xl text-bold">
                  Rp. 88,000
                </div>
              </div>
            </div>
          </q-card-section>

          <q-card-section>
            <div class="row q-mb-md">
              <div class="col-1">1x</div>
              <div class="col-8 text-bold text-uppercase">
                Egg and cheese muffin <br />
                <div class="text-harris text-sm text-uppercase">
                  Order note <br />
                  <div
                    class="text-weight-regular text-grey-7 text-lowercase text-sm"
                  >
                    Notes
                  </div>
                </div>
              </div>
              <div class="col-3 text-right">Rp. 43,000</div>
            </div>
            <div class="row">
              <div class="col-1">1x</div>
              <div class="col-8 text-bold text-uppercase">
                Ayam goreng khas rica <br />
              </div>
              <div class="col-3 text-right">Rp. 45,000</div>
            </div>

            <q-separator class="q-my-sm" />

            <div class="row">
              <div class="col-6 text-uppercase text-bold">Subtotal</div>
              <div class="col-6 text-right text-harris text-bold">
                Rp. 88,000
              </div>
            </div>
          </q-card-section>
        </q-card>
      </section>
    </div>

    <div class="container fixed-bottom payment">
        <div class="row q-pa-sm text-center items-center">
            <div class="col-6">
                <q-btn
                    class="full-width"
                    color="primary"
                    text-color="white"
                    unelevated
                    to="/"
                    label="PAYMENT"
                    no-caps
                />
            </div>
            <div class="col-6">
                <q-btn 
                    flat
                    color="white"
                    class="text-xl"
                    icon="monetization_on"
                />
            </div>
        </div>
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
// import { useRouter, useRoute } from "vue-router";

export default defineComponent({
  name: "MyOrder",

  setup({ root }) {
    //   const router = useRouter()

    const state = reactive({
      title: "Egg And Cheese Muffin",
      notes: "Perpaduan scrambled edd dan keju gurih dalam setangkup muffin",
      showMinus: false,
      angka: 0,
      minus: false,
      data: {},
      edit: "",
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
      alert("Router to detail food");
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

.payment {
    background-color: $primary;
}
</style>