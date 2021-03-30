<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar class="bg-white">
        <q-toolbar-title>
          <div class="text-bold text-primary">HIGH INOVATION</div> 
        </q-toolbar-title>

        <div class="q-pa-md">
          <q-btn
            flat
            rounded
            unelevated
            class="bg-primary"
            @click="onClickContact()" >
            <div class="q-px-md q-py-sm text-bold text-capitalize text-white">Contact</div>
          </q-btn>
        </div>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>



export default {
  name: 'MainLayout',
  data () {
    return { }
  }, 
  methods: {
    onClickContact () {
      const el = document.getElementById('footer');

      if (el) {
        el.scrollIntoView({behavior: 'smooth'});
      }
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