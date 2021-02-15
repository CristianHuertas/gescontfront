<template>
  <div>
    <Crear_gestion />

  
    <div id="lista_gestiones">
      <h3>ULTIMAS GESTIONES AL CLIENTE</h3>
      <table id="tabla1">
        <tr id="tabla_gestiones">
          <th>FECHA</th>

          <th>GESTOR</th>
          <th>TIPIFICACION</th>
          <th>RESUMEN DE LA GESTION</th>
        </tr>

        <tr
          v-for="gestion in database_gestiones"
          v-bind:key="gestion.id"
          id="tabla_gestiones2"
        >
          <td>{{ gestion.fecha_gestion }}</td>
          <td>{{ gestion.gestor }}</td>
          <td>{{ gestion.tipificacion }}</td>
          <td>{{ gestion.resumen_gestion }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>


<script>
import axios from "axios";
import Crear_gestion from "./Crear_gestion.vue";

export default {
  name: "Gestiones",
  data: function () {
    return {
      database_gestiones: [],
      datosJSON: {},
      username: "",
      id_cliente: "",
      gestor: "",
      tipificacion: "",
      resumen_gestion: "",
      fecha_gestion: "",
    };
  },
  components: { Crear_gestion },

  created: function () {
    this.username = this.$route.params.username;
  },
  beforeCreate: function () {
    this.id = localStorage.getItem("idbusqueda");
    

    /* axios.get("https://gescontbackend.herokuapp.com/gestion/registrosOrdenados/") */
    axios.get("https://gescontbackend.herokuapp.com/gestion/registroGetAll/" + this.id)
      
      .then((respuesta2) => {
        this.database_gestiones = respuesta2.data;
      })
      .catch((error) => {
        console.log(error);
        alert("no hay gestiones del cliente " + error.response.status);
      });
  },
 
};
</script>

<style>
</style>
