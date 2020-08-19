<template>
  <div id="app">
    <b-navbar toggleable sticky type="dark" variant="dark">
      <b-navbar-brand id="titulo" href="#">Citas Dostor</b-navbar-brand>
      <b-navbar-brand v-if="user" id="username" href="#">Hola, {{user.name}} </b-navbar-brand>
      <b-avatar v-if="user" :src="user.imageurl"></b-avatar>

      <b-navbar-toggle target="navbar-toggle-collapse">
        <template v-slot:default="{ expanded }">
          <b-icon v-if="expanded" icon="chevron-bar-up"></b-icon>
          <b-icon v-else icon="chevron-bar-down"></b-icon>
        </template>
      </b-navbar-toggle>

      <b-collapse id="navbar-toggle-collapse" is-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-item class="items" href="#"><router-link tag="b-nav-item" v-bind:to="{ name: 'auth' }">Login</router-link></b-nav-item>
          <b-nav-item class="items" v-if="user" href="#"><router-link tag="b-nav-item" v-bind:to="{ name: 'success' }">Listado de citas</router-link></b-nav-item>
          <b-nav-item class="items" v-if="user" href="#"><router-link tag="b-nav-item" v-bind:to="{ name: 'agendar' }">Agendar</router-link></b-nav-item>
          <b-nav-item class="items" v-if="user" @click.prevent="logout" href="#"><router-link tag="b-nav-item" v-bind:to="{ name: 'auth' }">Salir</router-link></b-nav-item>
        </b-navbar-nav>
      </b-collapse>
   </b-navbar>
    <br>
    <br>
    <br>
    <router-view />    
  </div>
</template>

<script>
export default {
  name: 'App',
  computed:{
    user(){
      return this.$store.state.user;
    }
  },
  methods:{
    logout(){
      this.$store.dispatch('logout');

    }
  }
  
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Alata&display=swap');

.items{
  text-align: right;
}

#username{
  font-size: 0.8rem;
  margin-left: auto;
}




#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}


#titulo{
  font-family: 'Alata', sans-serif;
}

*{
  font-family: 'Alata', sans-serif;
}



</style>