<template>
  <div id="app">
    <!-- nav bar -->
    <nav class="navbar has-background-link-light" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <router-link to="/" class="navbar-item is-size-3">
          <span class="icon">
            <i class="fa fa-book mr-2"></i>
          </span>
          <strong>Study Time</strong>
        </router-link>

        <a
          role="button"
          class="navbar-burger"
          aria-label="menu"
          aria-expanded="false"
          data-target="navbarBasicExample"
        >
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div class="navbar-menu mx-2">
        <div class="navbar-end">
         
          <div  class="navbar-item">
           <router-link to="/">
              <span class="icon">
                <i class="fa fa-table"></i>
              </span>
              <strong>Home</strong>
           </router-link>
          </div>
           <div class="navbar-item">
            <router-link to="/news">
              <span class="icon">
                <i class="fa fa-user-circle"></i>
              </span>
              <strong>Notification</strong>
              </router-link>
            
          </div>
          <div class="navbar-item" @click="logOut()">
            <span class="icon">
              <i class="fa fa-sign-out"></i>
            </span>
            <strong>LogOut</strong>
            
          </div>
          
          <!-- <div  class="navbar-item">
            <router-link to="/user/login">
              <span class="icon">
                <i class="fa fa-sign-in"></i>
              </span>
              <strong>Login</strong>
            </router-link>
          </div> -->
          
        </div>
      </div>
    </nav>
    
    
    <router-view :key="$route.fullPath" @auth-change="onAuthChange" :user="user" />
     <!-- <router-view :key="$route.fullPath" /> -->
  </div>
</template>

<script>
import axios from '@/plugins/axios'
export default {
  data () {
    return {
      user: null,
      }
  },
   mounted () {
    this.onAuthChange()
  },
  methods: {
    onAuthChange () {
      const token = localStorage.getItem('token')
      if (token) {
        this.getUser()
      }
    },
    getUser () {
      const token = localStorage.getItem('token')
      axios.get('/user/login').then(res => {
        this.user = res.data
      })
    },
    logOut(){
      this.$router.push({ name: 'login'})
    }
  },
};

</script>