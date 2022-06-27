<template>
<div>
  <v-layout :wrap="true" >
    <v-flex xs12>
        <p class="display-3" >Currency price BROU </p>
    </v-flex>
  </v-layout>
  <v-bottom-navigation v-model="colorBG" :background-color="color" class="mt-3 py-2">
  
    <v-btn @click="currency = 'USD'">
      <img
        src="../assets/001-estados-unidos.png"
        alt="John"
      >
    </v-btn>
    <v-btn @click="currency = 'BRL'">
      <img
        src="../assets/002-brasil.png"
        alt="John"
      >
    </v-btn>
    <v-btn @click="currency = 'EUR'">
      <img
        src="../assets/004-union-europea.png"
        alt="John"
      >
    </v-btn>
    <v-btn @click="currency = 'ARS'">
       <img
        src="../assets/003-argentina.png"
        alt="John"
      >
    </v-btn>
  </v-bottom-navigation>
  <v-layout :wrap="true" class="justify-center ma-5">
     <v-flex xs6>
    
      <v-date-picker 
          v-model="fecha"
          full-width
          locale="es-MX"
          color="grey"
          dark
          :max="max"
          :min="min"
          @change="getDolar(fecha)"></v-date-picker>
    
    </v-flex>
  </v-layout>
  <v-layout :wrap="true" class="justify-center ma-5">
   <v-flex xs6>
      <v-card >
      <v-card-subtitle> Venta  </v-card-subtitle>
        <v-card-text class="display-1"> $ {{venta}} </v-card-text>
        <v-divider class="mx-4"></v-divider>
         <v-card-subtitle> Compra  </v-card-subtitle>
        <v-card-text class="display-1">$ {{compra}}</v-card-text>
      </v-card>
    </v-flex>
    
  </v-layout>
    
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
import {mapMutations} from 'vuex';

export default {
  name: 'HomeView',
 data(){
    return{
      fecha:new Date().toISOString().substr(0,10), //comienza con la fecha del dia por defecto
      min:"1999",
      max: new Date().toISOString().substr(0,10), //como maximo la fecha del dia
      venta: null,
      compra:null,
      currency:null,
      colorBG: 0
    }

 },
 methods:{
  ...mapMutations(['mostrarLoading','ocultarLoading']),
  async getDolar(dia){
    try {
      this.mostrarLoading({titulo:'Loading data'});
      let datos = await axios.get(`https://cotizaciones-brou.herokuapp.com/api/currency/${dia}`)
      switch (this.currency) {
        case 'USD':
           this.venta = await datos.data.rates.USD.sell
           this.compra = await datos.data.rates.USD.buy
          break;
        case 'ARS':
           this.venta = await datos.data.rates.ARS.sell
           this.compra = await datos.data.rates.ARS.buy
          break;
        case 'EUR':
           this.venta = await datos.data.rates.EUR.sell
           this.compra = await datos.data.rates.EUR.buy
          break;
        case 'BRL':
           this.venta = await datos.data.rates.BRL.sell
           this.compra = await datos.data.rates.BRL.buy
          break;
      
        default:
          this.venta = await datos.data.rates.USD.sell
           this.compra = await datos.data.rates.USD.buy
          break;
      }
     
    } catch (error) {
     //
    }finally{
      this.ocultarLoading()
    }
    
  },
  formatear(fecha){
    let arrayFecha = fecha.split(['-']);
    let newFormato = arrayFecha[2] + '-' + arrayFecha[1] + '-' + arrayFecha[0];
    return newFormato;
  }
 },
 computed:{
   color () {
        switch (this.colorBG) {
          case 0: return 'red'
          case 1: return 'light-green lighten-1'
          case 2: return 'deep-purple darken-4'
          case 3: return 'blue lighten-3'
          default: return 'red'
        }
   }
 },
 watch:{
  currency:  function(){
    return this.getDolar(this.fecha)
  }
 },
 mounted() {
    this.getDolar(this.fecha);
 }
}
</script>
