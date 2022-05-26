<template>
  <div>
      <h1 class="text-center my-5">TodoList</h1>
      <div v-if="login" class="from-sc d-flex justify-content-center flex-column text-center">
            <input v-model="logintry.nickname" type="text" placeholder="Nickname">
            <input  v-model="logintry.password" type="password" placeholder="Password">
            <button @click="tryLog" class="mb-3 btn btn-dark">Login!</button>
            <span class="err" v-if="error">Inserisci i dati giusti oppure registrati</span>
            <span class="forLink" @click="logForm">Registrati!</span>
      </div>
      <div v-else class="from-sc d-flex justify-content-center flex-column text-center">
            <span class="text-star">Nickname</span>
            <input v-model="register.nickname" type="text" >
            <span class="text-star">Password</span>
            <input v-model="register.pw" type="password" >
            <span class="text-star">Nome</span>
            <input v-model="register.name" type="text" >
            <span class="text-star">Cognome</span>
            <input v-model="register.lastName" type="text">
            <button @click="registration" class="mb-3 btn btn-dark">Registrati!</button>
            <span class="err" v-if="error">Inserisci tutti i dati richiesti</span>
            <span class="forLink" @click="logForm">Login!</span>
      </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    name:"ApplLogin",
    components:{
    },
    data() {
        return {
            login: true,
            logged: false,
            logger:{},
            error: false,
            logintry : {
                nickname: "",
                password: "",
            },
            register : {
                nickname : "",
                pw : "",
                name: "",
                lastName: "",
                list: []
            },
            endpoint: "http://localhost:3000/accounts/"
        }
    },
    methods: {
        //choose form function
        logForm(){
            this.error = false
            this.login = !this.login
        },
        //register
        registration(){
            if(!(this.register.name.trim() ==="") && !(this.register.nickname.trim() ==="") && !(this.register.pw.trim() ==="") && !(this.register.lastName.trim() === "")){
                axios.post(this.endpoint, this.register)
                .then(r=>{
                    console.log(r.data)
                    this.error = false
                    this.logForm()
                })
            }else{
                this.error = true
            }
        },
        //login function
        tryLog(){
            axios.get(this.endpoint)
            .then(r=>{
                console.log(r.data)
                r.data.forEach(acc =>{
                    if(acc.nickname === this.logintry.nickname){
                        if(acc.pw === this.logintry.password){
                            this.logged = true
                            this.error = false
                            this.emiter(acc)
                        }
                    }else{
                        if(r.data.length == acc.id && !this.logged){
                            this.error = true
                        }
                    }
                })
                })
        },
        emiter(acc){
            this.$emit('approve', [true, acc])
        }
    },
  
   
}
</script>

<style lang="scss">
h1{
    font-weight: bold;
    text-transform: uppercase;
}

.from-sc{
    width: 300px;
    margin: auto;
    input{
        margin: 20px 0;
    }
    .forLink{
        color: blue;
        cursor: pointer;
    }
    .err{ 
        color: red;
    }
}

</style>