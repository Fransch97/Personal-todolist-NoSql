<template>
  <div id="app">
    
    <AppLogin v-if="!logged"  @approve="aprover"/>
    <div v-else>
    </div>
  </div>
</template>

<script>
import AppLogin from './components/AppLogin.vue';

export default {
  name: 'App',
  components: {
    AppLogin
  },
  data() {
    return {
      logged :false
    }
  },
  methods: {
    aprover(bool){
      this.logged = bool
    }
  },
}
</script>

<style lang="scss">
@import './assets/styles/global';





</style>
