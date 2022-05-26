<template>
  <div id="app">
    <!-- to login -->
    <AppLogin v-if="!logged"  @approve="aprover"/>
    
    <!-- logged -->
    <div v-else>
      <AppHeader :acc="acc" />
      <AppMain :acc="acc"/>
    </div>
  
  
  </div>
</template>

<script>
import AppLogin from './components/AppLogin.vue';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';

export default {
  name: 'App',
  components: {
    AppLogin,
    AppHeader,
    AppMain
},
  data() {
    return {
      logged :false,
      acc :{}
    }
  },
  methods: {
    aprover(arr){
      this.logged = arr[0]
      this.acc = arr[1]
    }
  },
}
</script>

<style lang="scss">
@import './assets/styles/global';





</style>
