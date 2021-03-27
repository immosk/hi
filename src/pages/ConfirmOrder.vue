<template>
  <q-page>
    <div class="q-pa-md">
      <p class="text-h5 text-bold text-uppercase text-harris">
        Confirm <br />
        Order
      </p>
      <p class="q-mb-md">NO. <span class="text-bold"> #1</span></p>
      <div class="text-uppercase text-sm">Customer Detail</div>
      <div class="row">
        <div class="col-4">
          <div class="text-uppercase text-bold">Name :</div>
          <div class="text-uppercase text-bold">Table :</div>
        </div>
        <div class="col-6">
          <div class="text-uppercase text-bold text-harris">Bala</div>
          <div class="text-uppercase text-bold">10</div>
        </div>
      </div>

      <section>
        <div class="row items-start q-gutter-md">
          <q-card class="my-card" flat bordered>
            <q-card-section horizontal>
              <q-card-section>
                <p class="text-bold text-uppercase">{{ title }}</p>
                <!-- <p>{{ notes }}</p> -->
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
                      color="grey-10"
                      size="sm"
                      icon="create"
                      v-model="edit"
                      @click="dialogAddNote = true"
                    />
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
                class="col-5 cover float-right"
                src="~assets/food_1.png"
              />
            </q-card-section>
          </q-card>
        </div>

        <q-separator class="q-my-md" />
        <div class="row">
          <div class="col">
            <div class="text-uppercase text-bold">Subtotal</div>
          </div>
          <div class="col">
            <div class="text-uppercase text-bold text-right">Rp. 88,000</div>
          </div>
        </div>
        <div class="row">
          <div class="text-xs text-bold text-red-10 col-6">
            *Please check your item before confirm order
          </div>
        </div>
      </section>

      <q-dialog v-model="dialogAddNote" persistent>
        <q-card style="min-width: 350px">
          <q-card-section>
            <div class="text-h6">Add Note</div>
          </q-card-section>

          <q-card-section class="q-pt-none">
            <q-input
              dense
              v-model="addNotes"
              autofocus
              @keyup.enter="dialogAddNote = false"
            />
          </q-card-section>

          <q-card-actions align="right" class="text-primary">
            <q-btn flat label="Cancel" v-close-popup />
            <q-btn unelevated color="primary" label="Save" v-close-popup />
          </q-card-actions>
        </q-card>
      </q-dialog>

      <q-btn
        class="q-mt-xl"
        color="primary"
        text-color="white"
        unelevated
        to="/my-order"
        label="Confirm Order"
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
  name: "ConfirmOrder",

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
      dialogAddNote: false,
      addNotes: "",
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
</style>