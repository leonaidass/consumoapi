<template>
  <div>
    <h1>Panel Administrador</h1>
    <v-container>
      <v-row>
        <v-col cols="4">
          <v-card class="siderbar pa-4 ">
            <h3>Agregar producto</h3>
            <v-text-field v-model="productoNuevo.nombre" label="Nombre"></v-text-field>
            <v-text-field v-model.number="productoNuevo.precio" label="Precio"></v-text-field>
            <v-text-field v-model.number="productoNuevo.cantidad" label="Cantidad"></v-text-field>
            <v-btn class="primary" @click="enviarPost()">Enviar</v-btn>
          </v-card>
        </v-col>
        <v-col>
            <v-card>
          <v-data-table
            :headers="headers"
            :items="productos"
            :items-per-page="5"
            class="elevation-1"
          >
          <template v-slot:item.total="{item}">
                 {{item.precio * item.cantidad}}
          </template>
             <template v-slot:item.acciones = "{item}">
                 <v-btn @click="eliminar(item.id)" color="red" dark>Eliminar</v-btn>
                 
                 </template>
          </v-data-table>
            </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import axios from "axios"
export default {
  data() {
    return {
      productos: [],
       headers: [
          
          { text: 'Nombre', value: 'nombre' },
          { text: 'Precio', value: 'precio' },
          { text: 'Cantidad', value: 'cantidad'},
          {text:'Total', value:'total'},
          {text:'Acciones', value:'acciones'}
       ],
       productoNuevo:{
           nombre:"",
           precio:0,
           cantidad:0,

        }
       }
    
  },
  methods: {
    obtenerproductos() {
      fetch("https://61afe8ff3e2aba0017c4959a.mockapi.io/productos")
        .then((res) => res.json())
        .then((res) => {
          this.productos = res;
        });
    },
    enviarPost(){
        // const encabezado = {
        //     method:"POST",
        //     headers:{"Content-Type": "application/json"},
        //     body:JSON.stringify(this.productoNuevo)
        // };
    //    fetch ("https://61afe8ff3e2aba0017c4959a.mockapi.io/productos",encabezado)
    //    .then((res)=> res.json())
    //    .then((data) =>{
    //        this.obtenerproductos()
    //        console.log(data)
    //    })
       axios.post(`https://61afe8ff3e2aba0017c4959a.mockapi.io/productos/`,this.productoNuevo)
           .then((data) =>{
           this.obtenerproductos()
           console.log(data)
       })

    },
    eliminar(id){
         let valor=id;
        // const encabezado = {
        //     method:"DELETE",
            
        // };
    //    fetch (`https://61afe8ff3e2aba0017c4959a.mockapi.io/productos/${valor}`,encabezado)
    //    .then((res)=> res.json())
    //    .then((data) =>{
    //        this.obtenerproductos()
    //        console.log(data)
    //    })
       axios.delete(`https://61afe8ff3e2aba0017c4959a.mockapi.io/productos/${valor}`)
       .then((data)=>{
           console.log(data)
           this.obtenerproductos();
       })

    }
  },
  mounted() {
    this.obtenerproductos();
  },
};
</script>

<style lang="scss" scoped></style>
