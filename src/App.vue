<template>
  <div>
    <div v-if="auth === false">
      <login @enter="checkLogin"/>
    </div>
    <div v-else>
      <cajero/>
    </div>
  </div>
</template>

<script>
import Cajero from './components/Cajero.vue'
import Login from './components/Login.vue'
import { async } from 'q';

export default {
  name: 'app',
  components: {
    Cajero,
    Login
  },
  data() {
    return {
      auth: false,
      usuarios: []
    }
  },
  mounted(){
    this.cargarUsuarios(),
    this.loadUsers()
  },
  methods:{
    cargarUsuarios(){
      console.log('cargar usuarios')
    },
    validar( pass ){
      const cantidadUsuarios = this.usuarios.length
      for (let i=0; i < cantidadUsuarios ; i++){
        console.log (this.usuarios[i].contraseña)
      }
    },
    loadUsers: async function(){
      const data = await fetch('./usuarios.json')
      this.usuarios = await data.json()
    },
    checkLogin(user) {
      // eslint-disable-next-line
      console.log(user.name)
      this.auth = true
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');
  body {
    margin: 0;

    font-family: "Source Sans Pro", sans-serif;

    background-color: #2a333d;
}
</style>
