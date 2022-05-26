<template>
  <main>
      <div class="container">
          <div class="mainheader">
                <p>Aggiungi qualcosa da fare</p>
                <div class="add">
                    <input v-model="newlist.name"  @keyup.enter="addTodo()" type="text">
                    <button class="btn btn-dark" @click="addTodo() ">vai</button>
                </div>
          </div>
          <div class="todo" v-for="(item, index ) in acc.list" :key="index">
                <span :class=" item.done === true ? 'done':''">{{item.name}}</span> 
                <div> 
                <span class="btn btn-dark mx-2" @click="done(index)">&#10004;</span>
                <span class="btn btn-dark" @click="deleteTodo(item.name)">&#128465;</span>
                </div>
            </div>
        </div>
  </main>
</template>

<script>
import axios from 'axios'
export default {
name:"AppMain",
props:{
    acc:Object,
},
methods: {
    addTodo(){
        this.actualAcc.list.push({...this.newlist})
        this.putAxios(this.actualAcc)
    },
    deleteTodo(param){
        this.actualAcc.list.forEach((list, index) => {
            if(list.name === param){
                 this.actualAcc.list.splice(index, 1)
            }
        });
        this.putAxios(this.actualAcc)
    },
    done(la){
        if(this.actualAcc.list[la].done === false){this.actualAcc.list[la].done = true}
        else{this.actualAcc.list[la].done = false}
        this.putAxios(this.actualAcc)
    },
    putAxios(param){
        axios.put(this.endpoit + this.acc.id , param)
        .then(r=>{
            console.log(r.data.list)
        })
    },


},
data() {
    return {
        endpoit: "http://localhost:3000/accounts/",
        newlist:{
            done: false,
            name: ""
        },
        actualAcc: this.acc
    }
},
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