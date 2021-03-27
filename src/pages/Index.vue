<template>
  <q-page>
    <div class="row">
      <div class="col text-center">
        <img class="" src="~assets/logo_harris.svg" />
        <p class="text-bold text-h5 text-uppercase q-mt-md text-harris">
          Harris Restaurant
        </p>
        <p>Good Morning, <span class="text-bold"> BALA</span></p>
      </div>
    </div>

    <section>
      <div class="q-pa-md">
        <q-carousel arrows animated v-model="slide" height="186px">
          <q-carousel-slide
            name="first"
            img-src="~assets/breakfast_1.png"
            class="rounded-xl"
          >
            <div
              class="absolute-center custom-caption full-width full-height rounded-xl"
            >
              <div class="row q-mt-xl">
                <div class="col items-center">
                  <div
                    class="text-h4 text-bold text-center text-harris text-uppercase"
                  >
                    50% OFF
                  </div>
                  <div class="text-h6 text-center text-white text-uppercase">
                    Breakfast Menu
                  </div>
                  <div
                    class="text-center text-caption text-white text-uppercase"
                    style="font-size: 0.75em"
                  >
                    *Syarat dan ketentuan berlaku
                  </div>
                </div>
              </div>
            </div>
          </q-carousel-slide>
          <q-carousel-slide
            name="second"
            img-src="~assets/breakfast_2.png"
            class="rounded-xl"
          >
            <div
              class="absolute-center custom-caption full-width full-height rounded-xl"
            >
              <div class="row q-mt-xl">
                <div class="col items-center">
                  <div
                    class="text-h4 text-bold text-center text-harris text-uppercase"
                  >
                    50% OFF
                  </div>
                  <div class="text-h6 text-center text-white text-uppercase">
                    Breakfast Menu
                  </div>
                  <div
                    class="text-center text-caption text-white text-uppercase"
                    style="font-size: 0.75em"
                  >
                    *Syarat dan ketentuan berlaku
                  </div>
                </div>
              </div>
            </div>
          </q-carousel-slide>
          <q-carousel-slide
            name="third"
            img-src="~assets/breakfast_3.png"
            class="rounded-xl"
          >
            <div
              class="absolute-center custom-caption full-width full-height rounded-xl"
            >
              <div class="row q-mt-xl">
                <div class="col items-center">
                  <div
                    class="text-h4 text-bold text-center text-harris text-uppercase"
                  >
                    50% OFF
                  </div>
                  <div class="text-h6 text-center text-white text-uppercase">
                    Breakfast Menu
                  </div>
                  <div
                    class="text-center text-caption text-white text-uppercase"
                    style="font-size: 0.75em"
                  >
                    *Syarat dan ketentuan berlaku
                  </div>
                </div>
              </div>
            </div>
          </q-carousel-slide>
        </q-carousel>
      </div>
    </section>

    <section>
      <div class="q-pa-md">
        <p class="text-center text-h6 text-bold text-uppercase text-harris">
          Menu 
        </p>

        <router-link to="/food">
          <q-card flat bordered class="q-mt-md rounded-xl">
            <q-img style="height: 89px" src="~assets/img_food.png">
              <div class="overlay">
                <div class="row items-center">
                  <div class="col-4">
                    <img src="~assets/icon_food.svg" />
                  </div>
                  <div class="col-8">
                    <p class="text-h5 text-bold text-right text-uppercase">
                      Food 
                    </p>
                    <p class="text-right">Choose your favorite food</p>
                  </div>
                </div>
              </div>
            </q-img>
          </q-card>
        </router-link>
      </div>
    </section>

    <section>
      <div class="q-pa-md">
        <p class="text-center text-h6 text-bold text-uppercase text-harris">
          Most Popular
        </p>
        <p class="text-center text-bold">Food & Beverage</p>
        
        <div class="row">
          <div class="col-xs-4 col-sm-3 col-md-6">
            <q-card @click="onClickNugget" flat bordered class="q-mt-md rounded-xl">
              <q-img style="height: 119px" src="~assets/popular_1.png">
                <div class="overlay">
                  <p class="text-bold text-uppercase">Nugget ayam</p>
                  <p class="text-xs">Most Popular</p>
                </div>
              </q-img>
            </q-card>
          </div>
        </div>
      </div>
      <p class="text-center text-xs text-bold text-uppercase text-grey-3 q-my-md">Thats all for now!</p>
    </section>
  </q-page>
</template>

<script>
import { defineComponent, reactive, toRefs, onMounted } from "@vue/composition-api";
import { Notify } from 'quasar';
import data from '../../data/data.json';

export default defineComponent({
  name: "PageFood",

  setup() {
    const state = reactive({
      slide: "first",
      title: "",
      data: [],
      tempData: "",
    });

    onMounted(() => {
      console.log('Data : ',data);
      const tempData = data['category'];
      console.log('tempData : ', tempData);
    })

    const onClickNugget = () => {
        // alert('Test Composition api Ok');
        Notify.create({
          type: "info",
          message: 'Quantity cannot be 0',
        });
    }

    return {
        ...toRefs(state),
        onClickNugget
    }
  },

});

</script>

<style lang="scss" scoped>



</style>