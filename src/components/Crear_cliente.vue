<template>
  <div id="d6">
    <div id="d7">
      <h3>Ingrese Los Datos Del Nuevo Cliente</h3>
      <form action="" id="nuevo_cliente">
        <label for="" id="n_documento">ID Cliente: </label>
        <input v-model="id_cliente" type="number"  class="etiqueta" minlength="1" maxlength="6" required>
        <br>

        <label for="" id="n_documento">Numero De Documento: </label>
        <input v-model="numeroDocumento" type="number"  class="etiqueta" minlength="8" maxlength="10" required>
        <br>

        <!-- <label for="" id="t_documento">Tipo de Documento: </label>
        <select id="selectorDocumento" ref="myId">
            <option value="" selected>NIT</option>
            <option value="">CEDULA</option>
        </select>
        <br> -->


        <label for="" id="razon_social">Razon social: </label>
        <input v-model="nombre" type="text" id="" required>
        <br>
        <label for="" id="contacto">Contacto: </label>
        <input v-model="contacto" type="text" id="" required>
        <br>
        <label for="" id="telefono">Telefono: </label>
        <input v-model="telefono" type="tel" id="" minlength="7" maxlength="10" required>
        <br>
        <!-- <label for="" id="direccion">Direccion: </label>
        <input v-model="direccion" type="text" id="" required>
        <br> -->
        <label for="" id="ciudad">Ciudad: </label>
        <input v-model="ciudad" type="text" id="" required>
        <br>
        <label for="" id="correo">Correo: </label>
        <input v-model="correo" type="email" id="" required>
        <br>
        <label for="" id="detalle">Detalle: </label>
        <input v-model="detalle" type="text" id="" >
        <br>

      </form>
      <button v-on:click="guardarCliente" >Crear Cliente</button>

    </div>
  </div>
</template>


<script>
import axios from "axios"

export default {
    name: "Crear_cliente",
    data(){
      return{
        id_cliente:"",
        numeroDocumento:"",
        tipoDocumento:"",
        nombre:"",
        contacto:"",
        telefono:"",
        ciudad:"",
        correo:"",
        detalle:"",
        datosJSON:{}
      }
    },
    methods:{
      guardarCliente: function(){
        /* if (this.$refs.myId.selectedIndex===0){
          this.tipoDocumento="NIT"
        }
        else if(this.$refs.myId.selectedIndex===1){
          this.tipoDocumento="CC"
        } */
        this.datosJSON={
          id_cliente: this.id_cliente,
          documento: this.numeroDocumento,
          tipo_documento: this.tipoDocumento,
          razon_social: this.nombre,
          contacto: this.contacto,
          telefono: this.telefono,
          ciudad: this.ciudad,
          correo: this.correo,
          detalle: this.detalle
        }
        console.log(this.datosJSON);
        axios.post("https://gescontbackend.herokuapp.com/cliente/registroSave/", this.datosJSON, {headers: {}})
        /* axios.post("http://localhost:8000/cliente/registroSave", this.datosJSON, {headers: {}}) */ /* crear un cliente */
        .then(respuesta=>{
          console.log(respuesta.data);
          alert("operacion exitosa")
        })
        .catch(error=>{
          console.log(error)
          alert("No se pudo agregar " + error.response.status)
          /* this.$router.push({name: "crudClientes"}); */
        })
      }
    }
}

</script>


<style>
#d6 {
  width: auto;
  height: auto;
  background-color: rgb(238, 238, 238);
}
#d7 {
  /* border: solid 1px #000000; */
  margin: 10px auto;
  width: 400px;
  height: auto;
  background-color: rgb(238, 238, 238);
  
}

#d7 h3 {
  text-align: center;
  margin: 10px 10px;
  font-size: 20px;
}
#d7 label {
  text-align: left;
  margin: 10px 10px;
  font-size: 18px;
}

#nuevo_cliente {
    font-size: 18px;
}

#d7 button{
  background: #133264;
  border: 0;
  border-radius: 3px;
  color: white;
  cursor: pointer;
  font-size: 15px;
  padding: 20px 25px;
  margin: 10% 25%;
}


</style>