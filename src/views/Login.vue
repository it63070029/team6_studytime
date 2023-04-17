<template>

 <div class="container is-fluid mt-5">
        <div class="columns is-centered">

        <div class="column is-4 mt-2">
            <h1 class="title">Log in</h1>

            <p v-if="error" class="px-3 py-2 mb-3 has-text-danger-dark has-background-danger-light">{{ error }}</p>

        <!-- Login form -->
        <div class="field mt-2">
          <label class="label">Username</label>
          <div class="control has-icons-left">
            <input v-model="username" class="input" type="text" />
            <span class="icon is-small is-left">
              <i class="fas fa-user"></i>
            </span>
          </div>
        </div>

        <div class="field mt-4">
          <label class="label">Password</label>
          <div class="control has-icons-left has-icons-right">
            <input v-model="password" class="input" type="password" />
            <span class="icon is-small is-left">
              <i class="fas fa-lock"></i>
            </span>
            <span class="icon is-small is-right">
              <i class="fas fa-check"></i>
            </span>
          </div>
        </div>

        <button class="button is-link is-fullwidth mt-3" @click="submit">
          Login
        </button>

      </div>
    </div>
  </div>
</template>

<script>
import axios from '@/plugins/axios'

export default {
  data () {
    return {
      username: '',
      password: '',
      error: '',
      listUser:[
        {id:1,username:"it63070029",password:"63070029",idStu:"63070029"},
        {id:2,username:"it63070030",password:"63070030",idStu:"63070030"},
        {id:3,username:"it63070031",password:"63070031",idStu:"63070031"},
        
      ],
      check_user:[]
    }
  },
  methods: {
    submit() {
      
      this.check_user = this.listUser.filter((val)=>val.username==this.username && val.password == this.password)
      console.log(this.check_user.length+"checkuser")
      // let check_password = thi.listUser.filter((val)=>val.password == this.password)
      if(this.check_user.length>0){
        this.$router.push({ name: 'home'})

      }
      else{
        alert("คุณกรอก Username หรือ Password ผิดกรุณากรอกใหม่")
      }
     }
   },
}
</script>