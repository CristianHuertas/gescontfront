<template>
  <div id="d4">
    <div id="d5">
      <h3>Datos Del Cliente Solicitado</h3>
      <table id="cliente">
        <tr>
          <th>ID cliente:</th>
          <td>{{ database_clientes.id_cliente }}</td>
        </tr>
        <tr>
          <th>Documento:</th>
          <td>{{ database_clientes.documento }}</td>
        </tr>
        <tr>
          <th>Razon Social:</th>
          <td>{{ database_clientes.razon_social }}</td>
        </tr>
        <tr>
          <th>Contacto:</th>
          <td>{{ database_clientes.contacto }}</td>
        </tr>
        <tr>
          <th>Telefono:</th>
          <td>{{ database_clientes.telefono }}</td>
        </tr>
       <!--  <tr>
          <th>Direccion:</th>
          <td>{{ database_clientes.direccion }}</td>
        </tr> -->
        <tr>
          <th>Ciudad:</th>
          <td>{{ database_clientes.ciudad }}</td>
        </tr>
        <tr>
          <th>Correo:</th>
          <td>{{ database_clientes.correo }}</td>
        </tr>
        <tr>
          <th>Observacion:</th>
          <td>{{ database_clientes.detalle }}</td>
        </tr>
      </table>
      <button v-if="0">Editar</button>
      <button v-if="0">Guardar</button>
    </div>
  <Gestiones />

  </div>
</template>




<script>
import axios from "axios";
import Gestiones from "./Gestiones.vue";

export default {
  name: "Datos_un_cliente",
  components: { Gestiones},
  data: function () {
    return {
      id: 0,
      database_clientes: {
        id_cliente: 0,
        documento: 0,
        tipo_documento: "",
        razon_social: "",
        contacto: "",
        telefono: 0,
        ciudad: "",
        correo: "",
        detalle: "",
      }
     };
  },
  beforeCreate: function () {
    this.id = localStorage.getItem("idbusqueda");

    axios.get("https://gescontbackend.herokuapp.com/cliente/registroGet/" + this.id)
      /* axios.get("http://localhost:8000/cliente/registroGet/"+this.id) */

      .then((respuesta) => {
        this.database_clientes = respuesta.data;
      })
      .catch((error) => {
        console.log(error);
        alert("cliente no existe " + error.response.status);
        /* this.$router.push({ name: "menu" }); */
      });
  }
};


</script>


<style>
#d4 {
  width: auto;
  height: auto;
  background-color: rgb(238, 238, 238);
}
#d5 {
  /* border: solid 1px #000000; */
  margin: 10px auto;
  width: 400px;
  height: auto;
  background-color: rgb(238, 238, 238);
}

#d5 h3 {
  text-align: center;
}

#cliente {
  text-align: left;
}
#cliente tr td {
  border: solid 1px #000000;
}

#d5 button {
  background: #456c99;
  border: 0;
  border-radius: 3px;
  color: white;
  cursor: pointer;
  font-size: 15px;
  padding: 20px 25px;
  margin: 20px 10%;
}

#caja_gestion {
  width: 70%;
  height: 80px;
  margin: 1% 15%;
  border-radius: 5px;
  font-size: 15px;
}

#nueva_gestion {
  width: 100%;
  text-align: center;
}

#boton_aceptar {
  margin: 1% 45%;
}

div table #tabla_gestiones th {
  border: solid 1px #000000;
}

#tabla_gestiones {
  border: solid 1px #000000;
  height: 20px;
  text-align: center;
  width: 200px;
}
#tabla_gestiones2 {
  border: solid 1px #000000;
  height: 20px;
  text-align: center;
}

#lista_gestiones {
  text-align: center;
  margin: 0 10%;
}

#tabla1 {
  width: 80%;
  margin: 0 10%;
}
</style>