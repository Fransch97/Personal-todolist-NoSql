<template>
  <header>
      <div class="container d-flex justify-content-between py-4">
            <div class="logo">Todo</div>
            <div class="acc d-flex">
                <div class="acc">{{acc.nickname}}</div>
                <div class="logout mx-4">Logout</div>
                
            </div>
      </div>
  </header>
</template>

<script>
export default {
    name: "AppHeader",
    props:{
        acc: Object
    }

}
</script>

<style lang="scss" scoped>
header{
    background-color: black;
    color: white;
    font-weight: bold;
    font-size: 25px;
}
</style>