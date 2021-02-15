<template>
  <div>
    <div id="nueva_gestion">
      <h3>INGRESE UNA NUEVA GESTION</h3>
      <form id="formulario_gestion" v-on:submit.prevent="guardarGestion">
        <textarea
          name="caja_gestion"
          form="formulario_gestion"
          id=""
          cols="130"
          rows="5"
          autocomplete="off"
          placeholder="INGRESE UN RESUMEN DE LA GESTION REALIZADA"
          required
          v-model="resumen_gestion"
        ></textarea>
        <br />
        <label for="" id="t_documento" ref="myId">Tipo de Gestion: </label>
        <select id="selectorDocumento" ref="myId">
          <option value="" selected>Seleccione una opcion</option>
          <option value="">Activacion / Suspension</option>
          <option value="">Acuerdo de pago</option>
          <option value="">Cambio de datos</option>
          <option value="">Conciliacion cartera</option>
          <option value="">Envío de correo</option>
          <option value="">Error operaciones</option>
          <option value="">Error comercial</option>
          <option value="">Error facturacion</option>
          <option value="">Ilocalizado</option>
          <option value="">Insolvente</option>
          <option value="">No contesta</option>
          <option value="">No reconoce la deuda</option>
          <option value="">Se dejo mensaje</option>
          <option value="">Sin contrato</option>
          <option value="">Sin presupuesto</option>
        </select>
        <br />
       <!--  <button id="boton_aceptar">Aceptar</button> -->
      <button>Aceptar</button>

      </form>
      
    </div>
  </div>
</template>

<script>
/* import Encabezado from './components/Encabezado.vue' */
import axios from "axios"

export default {
  name: "Crear_gestion",
  /* components: {Encabezado}, */
  data(){
      return{
        datosJSON2:{},
        id_gestion: 0,
        id_cliente: 0,
        fecha_gestion:"",
        gestor: "",
        tipificacion: "",
        resumen_gestion: "",
      }
    },
    methods: {
  guardarGestion: function(){
        if (this.$refs.myId.selectedIndex===0){
          this.tipificacion="Seleccione una opcion"
        }
        else if(this.$refs.myId.selectedIndex===1){
          this.tipificacion="Activacion / Suspension"
        }
        
        else if(this.$refs.myId.selectedIndex===2){
          this.tipificacion="Acuerdo de pago"
        }  
        else if(this.$refs.myId.selectedIndex===3){
          this.tipificacion="Cambio de datos"
        } 
        else if(this.$refs.myId.selectedIndex===4){
          this.tipificacion="Conciliacion cartera"
        } 
        else if(this.$refs.myId.selectedIndex===5){
          this.tipificacion="Envío de correo"
        } 
        else if(this.$refs.myId.selectedIndex===6){
          this.tipificacion="Error operaciones"
        } 
        else if(this.$refs.myId.selectedIndex===7){
          this.tipificacion="Error comercial"
        } 
        else if(this.$refs.myId.selectedIndex===8){
          this.tipificacion="Error facturacion"
        } 
        else if(this.$refs.myId.selectedIndex===9){
          this.tipificacion="Ilocalizado"
        } 
        else if(this.$refs.myId.selectedIndex===10){
          this.tipificacion="Insolvente"
        } 
        else if(this.$refs.myId.selectedIndex===11){
          this.tipificacion="No contesta"
        } 
        else if(this.$refs.myId.selectedIndex===12){
          this.tipificacion="No reconoce la deuda"
        } 
        else if(this.$refs.myId.selectedIndex===13){
          this.tipificacion="Se dejo mensaje"
        } 
        else if(this.$refs.myId.selectedIndex===14){
          this.tipificacion="Sin contrato"
        } 
        else if(this.$refs.myId.selectedIndex===15){
          this.tipificacion="Sin presupuesto"
        }  
        
        if (this.tipificacion!="Seleccione una opcion") {
                            
        this.id = localStorage.getItem("idbusqueda");
        this.gestor = localStorage.getItem("username");

        this.datosJSON2={
                 
          id_cliente: this.id,
          gestor: this.gestor,
          tipificacion: this.tipificacion,
          resumen_gestion: this.resumen_gestion         
        }
        
        console.log(this.datosJSON2);        
        axios.post("https://gescontbackend.herokuapp.com/gestion/registroSave/", this.datosJSON2, {headers: {}})
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
      }else{
          alert("Debe Seleccionar una tipificacion ")

      }
  }
    }
}
</script>



