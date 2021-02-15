<template>
  <div id="d1">
    <div id="crud">
      
      <form v-on:submit.prevent="cambiar_estado">
        <label for="nit"><b>ID Cliente:</b></label>
        <!-- <input/> -->
        <input v-model="idbusqueda" type="number" id="nit" placeholder="Solo datos numericos" minlength="1" maxlength="10" v-on:keyup.enter="cambiar_estado" @keypress="false" required/>        
      </form>
      
      <button id="buscar" @click="cambiar_estado">{{BuscarEtiqueta}} </button>   
     <!--  <button v-on:click="eliminarCliente" id="eliminar">Eliminar Cliente</button>  -->  
      <button class="crud" @click="ocultar_components">Crear Cliente</button>
      <button class="crud" @click="ocultar_components2">Modificar Cliente</button>

      
      
      
    </div> <!-- elige que componente usar -->
    <div id="interruptor2" v-if="estado1">
      <Base_clientes />
    </div>
    <div id="interruptor1"  v-if="estado2">
      <Datos_un_cliente />
    </div>
    <div id="interruptor3" v-if="estado3">
      <Crear_cliente/>
    </div>
    <div id="interruptor4" v-if="estado4">
      <Modificar_cliente/>
    </div>
    <Pie_pagina/>
  </div>
</template>

<script>
import Crear_cliente from './Crear_cliente.vue';
/* import Modificar_cliente from './Modificar_cliente.vue'; */
import Base_clientes from "./Base_clientes.vue";
import Datos_un_cliente from "./Datos_un_cliente.vue";
import Pie_pagina from './Pie_pagina.vue';
import axios from "axios"
import Modificar_cliente from './Modificar_cliente.vue';

export default {
  name: "Crud_clientes",
  components: { Base_clientes, Datos_un_cliente, Pie_pagina, Crear_cliente, Modificar_cliente },
  data() {
    return {
    BuscarEtiqueta: "Buscar",
    crearEtiqueta: "Crear/moificar Cliente",
    estado1: true,
    estado2: false,
    estado3: false,
    idbusqueda: 0,
    }
  },
  methods: {
    cambiar_estado(){
      if(this.estado2===true){
        this.BuscarEtiqueta= "Buscar";
        this.estado1 = true;
        this.estado2 = false;
        this.estado3 = false;
      }
      else{
        this.BuscarEtiqueta= "Volver";
        this.estado1 = false;
        this.estado2 = true;
        this.estado3 = false;
        localStorage.setItem("idbusqueda", this.idbusqueda);
      }
    },
    ocultar_components(){
      if(this.estado3===true){
        /* this.crearEtiqueta= "Crear/moificar Cliente"; */
        this.BuscarEtiqueta= "Volver";
        this.estado1 = true;
        this.estado2 = false;
        this.estado3 = false;
        this.estado4 = false;
      }
      else{
        /* this.crearEtiqueta= "volver"; */
        this.BuscarEtiqueta= "Volver";
        this.estado1 = false;
        this.estado2 = false;
        this.estado3 = true;
        this.estado4 = false;
      }
    },
    ocultar_components2(){
      if(this.estado4===true){
        /* this.crearEtiqueta= "Crear/moificar Cliente"; */
        this.BuscarEtiqueta= "Volver";
        this.estado1 = true;
        this.estado2 = false;
        this.estado3 = false;
        this.estado4 = false;
      }
      else{
        /* this.crearEtiqueta= "volver"; */
        this.BuscarEtiqueta= "Volver";
        this.estado1 = false;
        this.estado2 = false;
        this.estado3 = false;
        this.estado4 = true;
      }
    },
    eliminarCliente: function(){
      
      axios.delete("https://gescontbackend.herokuapp.com/cliente/registroDel/"+this.idbusqueda) 
      /* axios.delete("http://localhost:8000/cliente/registroDel/"+this.idbusqueda) */ /* Eliminar un cliente */

      .then(respuesta=>{
        console.log(respuesta.data);
        alert("se elimino el cliente con id "+this.idbusqueda+" de forma exitosa")
        this.$router.push({name: "crudClientes"});      
      })
      .catch(error=>{
        console.log(error)
        alert("El cliente no existe" + error.response.status)
        this.$router.push({name: "crudClientes"});     
      }) 
    }
  }

};
</script>

<style>
/* poner bordes para ver cuadricula */
/* #crud {
  border: solid 1px #000000;
} */
#d1 {
  /* border: solid 1px #000000; */

  width: auto;
  height: 95px;
  background-color: rgb(238, 238, 238);
  
}

#crud {
  margin: 0 auto;
  width: 80%;
  height: 90px;
  background-color: rgb(238, 238, 238);
}

#crud form {
  margin: 30px 30px;
  display: inline-block;
  vertical-align: middle;
  font-size: 21px;
}

#buscar {
  background: #456C99;
  border: 10;
  border-radius: 10px;
  color: white;
  cursor: pointer;
  font-size: 10px;
  padding: 8px 25px;
  margin: 0px;
  margin-right: 1%;
}

#eliminar{
  background: #456C99;
  border: 10;
  border-radius: 10px;
  color: white;
  cursor: pointer;
  font-size: 10px;
  padding: 8px 25px;
  margin: 0px;
  margin-right: 10%;
}
.crud{
  background: #456C99;
  border: 10;
  border-radius: 10px;
  color: white;
  cursor: pointer;
  font-size: 12px;
  padding: 20px 20px;
  margin: 0px 2px;
}
</style>

