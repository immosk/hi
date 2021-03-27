<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar class="bg-white">
        <q-btn
          flat
          dense
          round
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        >
          <img
            alt="menu"
            src="~assets/icon_menu.svg"
          >
        </q-btn>

        <q-toolbar-title>
          <!-- Quasar App -->
        </q-toolbar-title>

        <div class="q-pa-md">
          <q-btn
            flat
            dense
            round
            aria-label="Menu"
          >
            <img
              class=""
              alt="logo cart"
              src="~assets/icon_cart.svg"
            >
          </q-btn>
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-white"      
    >
      <q-list class="border-primary">
        <q-item-label
          header
          class="bg-white"
        >
          Essential Links
        </q-item-label>
        <EssentialLink
          class="bg-white"
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink.vue'

const linksData = [
  {
    title: 'Home',
    caption: 'Home',
    icon: 'home',
    link: '/'
  },
  {
    title: 'Food',
    caption: 'Food',
    icon: 'code',
    link: '/food'
  },
  {
    title: 'Beverage',
    caption: 'Beverage',
    icon: 'chat',
    link: '/beverage'
  },
  {
    title: 'Dessert',
    caption: 'Dessert',
    icon: 'record_voice_over',
    link: '/dessert'
  }
];

export default {
  name: 'MainLayout',
  components: { EssentialLink },
  data () {
    return {
      leftDrawerOpen: false,
      essentialLinks: linksData
    }
  }
}
</script>

<style lang="scss" scoped>
.border-primary {
  border-right-color: $primary;
  border-width: 5px;
  border-right-style: solid;
}
</style>