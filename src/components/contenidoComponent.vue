<template>
<div class="panel">
    <div class="encabezado">
                 <h1 class="texto">Personajes de Rick y Morty</h1>
            </div>


<div class="container"> 
          
            <div class="filtro">
               <b-form-input id="busqueda" v-model="busqueda" placeholder="Buscar personaje..." class="busqueda" v-on:keyup="filterNombres()"></b-form-input>
            </div>

            <div class="cards">
                  <b-card  v-for="(personajes, index) in listaPersonajes.slice((currentPage-1)*perPage,(currentPage-1)*perPage+perPage)" :key="index"
                          style="max-width: 20rem;"
                          class="text-center mb-4"
                          :footer="personajes.name">
                
                      <b-card-title id="circulo"> 
                          {{personajes.id}}
                      </b-card-title>
                
                        
                      <b-card-body id="cuadrado"> 
                          <div><img :src="personajes.image" alt=""></div> 
                      </b-card-body>
                        
                  </b-card>
            </div>


            <nav class="pagination">
               <b-pagination v-model="currentPage" :total-rows="listaPersonajes.length" :per-page="perPage" prev-text="Anterior" next-text="Siguiente"></b-pagination>
            </nav>
                       
</div>
</div>
</template>


<script>
import {Global} from '@/Global';
import axios from 'axios'; 

export default {
  name: "contenidoComponent",
  components: {
    
   },

  data () {
      return {
           busqueda: null,
           listaPersonajes: [],
           listaPersonajesAux:[],
           nombrePersonaje: null,
           currentPage: 1,
           perPage:2
      }
    
    },
   mounted:function() {
      this.obtenerPersonajes();
    },
   computed: {
     
    },
  
  methods: {
      obtenerPersonajes(){
        axios.get(Global.url + '/character').then( res => {
          if (res.status == 200){
            this.listaPersonajes = res.data.results;
            this.listaPersonajesAux = res.data.results;
            } 
           
          }) 
          .catch(error => {
             console.log(error);
          })
      },

      filterNombres (){
        this.listaPersonajes = this.listaPersonajesAux;
            this.listaPersonajes = this.listaPersonajes.filter(
              (nombre) => {   
                      return nombre.name.toUpperCase().includes(this.busqueda.toUpperCase())
                })  
      
      },

    }


  }

</script>

<style scoped>
@import '../assets/css/style.css';

.card-footer {
     font-family: inherit;
     text-transform: uppercase;
     font-size: 17px;
     color: white;
     font-weight: bold;
     background-color: #204d97;
     border: 2px solid #204d97;
 }

</style>
