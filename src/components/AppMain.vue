<template>
  <main>
      <div class="container">
          <div class="mainheader">
                <p>Aggiungi qualcosa da fare</p>
                <div class="add">
                    <input type="text">
                    <button class="btn btn-dark">vai</button>
                </div>
          </div>
          <div class="todo" v-for="item in acc.list" :key="item.id">
                <span :class=" item.done === true ? 'done':''">{{item.name}}</span> 
                <div> 
                <span class="btn btn-dark mx-2">&#10004;</span>
                <span class="btn btn-dark">&#128465;</span>
                </div>
            </div>
        </div>
  </main>
</template>

<script>
export default {
name:"AppMain",
props:{
    acc:Object
}
}
</script>

<style lang="scss" scoped>

main{
    margin: 0 auto;
    margin-top: 100px;
    padding: 20px 10px;
    width: 60%;
    min-width: 450px;
    background-color: aqua;
    border-radius: 20px;
    .mainheader{ 
        text-align: center;
        background-color: lightcyan;
        padding: 20px 0;
        .add{
            display: flex;
            justify-content: center;
            input{
                padding: 5px;
                width: 80%;
            }
        }
    }
        .todo{
            padding: 20px 50px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            background-color: rgb(252, 252, 252);
            .done{ 
                text-decoration: line-through;
            }
        }
}

</style>