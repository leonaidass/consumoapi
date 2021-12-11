<template>
  <div class="home">
    <!-- <v-btn @click="obtenerproductos()" class="primary mt-2" >Obtener Datos</v-btn> -->
    <v-container>
       <v-row>
         <v-col cols="12" md="4" v-for="producto in productos" :key="producto.id">
           <v-card>
             <v-card-title>
               {{producto.nombre}}
             </v-card-title>
             <v-card-text>
               <img :src=producto.imagen alt="" style="width:50%">
               <p>Precio: {{producto.precio}}</p>
               <p>Cantidad: {{producto.cantidad}}</p>
               

             </v-card-text>
           </v-card>
         </v-col>
       </v-row>
    </v-container>
    
  </div>
</template>

<script>
// @ is an alias to /src


export default {
  name: 'Home',
  data() {
    return {
      productos:[]
    }
  },
  methods:{
    obtenerproductos(){
        fetch("https://61afe8ff3e2aba0017c4959a.mockapi.io/productos")
        .then(res => res.json())
        .then(datos =>{
          this.productos=datos
        })
    }
  },
  mounted(){
    this.obtenerproductos()
  }
 
  
}
</script>
