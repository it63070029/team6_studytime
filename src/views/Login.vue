<template>
<div>
  <h3>Login</h3>
</div>
</template>

<script>
import axios from '@/plugins/axios'

export default {
  data () {
    return {
      username: '',
      password: '',
      error: ''
    }
  },
  methods: {
    submit() {
    //   const data = {
    //     username: this.username,
    //     password: this.password
    //   }

    //   axios.post('http://localhost:3000/user/login', data)
    //     .then(res => {
    //       const token = res.data.token                                
    //       localStorage.setItem('token', token)
    //       this.$emit('auth-change')
    //       this.$router.push({path: '/'})
    //     })
    //     .catch(error => {
    //       this.error = error.response.data
    //       console.log(error.response.data)
    //     })
     }
   },
}
</script>