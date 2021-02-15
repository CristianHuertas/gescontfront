<template>
  <div id="cuadro_logueo_1">
    <div id="cuadro_logueo_2">
      <div id="cuadro_logueo_3">
        <h3>LOGIN</h3>
        <form id="login" v-on:submit.prevent="autenticar">
          <h5>Ingrese usuario y contraseña</h5>
          <input
            type="text"
            v-model="username"
            class="etiqueta_login"
            placeholder="USUARIO"
            required
          />
          <input
            type="password"
            v-model="password"
            class="etiqueta_login"
            placeholder="CONTRASEÑA"
            required
          />
        <button>Iniciar Sesion</button>

          <!-- <button v-on:click="Ingresar_login">Aceptar</button> -->
        </form>
        <!-- <button @click="autenticar">Iniciar Sesion</button> -->
      </div>
    </div>

    <Pie_pagina />
  </div>
</template>


<script>
import axios from "axios";
import Pie_pagina from "./Pie_pagina.vue";

export default {
  name: "login",
  data: function () {
    return {
      username: "",
      password: "",
      users: {},
    }
  },
  components: { Pie_pagina },
  methods: {
    Ingresar_login: function () {
      if (this.$router.name != "crudClientes") {
        this.$router.push({ name: "crudClientes" });
      }
    },
    autenticar: function () {
      localStorage.setItem("username", this.username);
      this.users={
        username: this.username,
        password: this.password
      }

      /* this.username = username; */
      console.log(this.users);

      axios
        .post("https://gescontbackend.herokuapp.com/user/auth/", this.users, {headers: {}}) /* consultar usuario y contraseña */
        /* axios.get("http://localhost:8000/cliente/registroGet/"+this.id) */

        .then((respuesta) => {
          console.log(respuesta.data);

          this.$router.push({ name: "crudClientes" });
        })
        .catch((error) => {
          console.log(error);
          
          if (error.response.status == 404) {
            alert("El usuario no existe " + error.response.status);
            
          }else if (error.response.status == 403) {
          alert("Contraseña Incorrecta " + error.response.status);
            
          }    
        })
    },
  },
};
</script>

<style>
#cuadro_logueo_1 {
  width: auto;
  height: auto;
  background-color: white;
}

#cuadro_logueo_2 {
  width: auto;
  height: auto;
  margin: 8% 10%;
  background-color: white;
}

#cuadro_logueo_3 {
  width: 20%;
  height: auto;
  background-color: rgb(40, 105, 85);
  margin: 5% 40%;
  text-align-last: center;
}

#login {
  color: aliceblue;
  height: 150px;
  margin: 10% 0%;
}

#cuadro_logueo_2 h3 {
  color: aliceblue;
}

#login .etiqueta_login {
  color: black;
  margin: 2% 20%;
  height: auto;
  width: 60%;
}
</style>