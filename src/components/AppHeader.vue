<template>
  <header>
      <div class="container d-flex justify-content-between py-4">
            <div class="logo">Todo</div>
            <div class=" d-flex">
                <div class="acc">{{acc.nickname}}</div>
                <div class="logout mx-4" @click="logout()">Logout</div>
                
            </div>
      </div>
  </header>
</template>

<script>
export default {
    name: "AppHeader",
    props:{
        acc: Object
    },
    methods: {
        logout(){
        this.actualAcc = {}
        this.$emit('logout', "bye")
    }
    },

}
</script>

<style lang="scss" scoped>
header{
    background-color: black;
    color: white;
    font-weight: bold;
    font-size: 25px;
    .logout{
        cursor: pointer;
    }
    .acc{
        text-transform: capitalize;
    }
}
</style>