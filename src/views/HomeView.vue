<template>
<div>

  <v-layout :wrap="true">
    <v-flex xs12>
      <v-card color="dark" dark>
        <v-card-text class="display-1">Cotizaciónes brou</v-card-text>
      </v-card>
    </v-flex>
  </v-layout>
  <v-bottom-navigation>
    <v-btn @click="currency = 'USD'">
      <span>USD</span>
    </v-btn>
    <v-btn @click="currency = 'BRL'">
      <span>BRL</span>
    </v-btn>
    <v-btn @click="currency = 'EUR'">
      <span>EUR</span>
    </v-btn>
    <v-btn @click="currency = 'ARS'">
      <span>ARS</span>
    </v-btn>
  </v-bottom-navigation>
  <v-layout :wrap="true" class="justify-center ma-5">
     <v-flex xs12>
     <v-card >
      <v-date-picker 
          v-model="fecha"
          locale="es-MX"
          color="grey"
          :max="max"
          :min="min"
          @change="getDolar(fecha)"></v-date-picker>
     </v-card>
    </v-flex>
  </v-layout>
   <v-flex xs12>
      <v-card color="dark" dark>
        <v-card-text class="display-2"> Venta: $ {{venta}} -- Compra : $ {{compra}}</v-card-text>
      </v-card>
    </v-flex>
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
    }

 },
 methods:{
  ...mapMutations(['mostrarLoading','ocultarLoading']),
  async getDolar(dia){
    try {
      console.log(this.currency);
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
