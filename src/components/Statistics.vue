<template>
    <div>
    <h1 class="display-3">Price history</h1>
          <v-card
    class="mt-4 mx-auto"
    max-width="80%"
  >
  <v-card-title>
       Fluctuation of the {{currency}} in 21-22
  </v-card-title>
    <v-sheet
      class="v-sheet--offset mx-auto"
      color="cyan"
      elevation="12"
      max-width="calc(100% - 32px)"
    >
      <v-sparkline
        :value="value"
        color="white"
        line-width="2"
        padding="16"
      ></v-sparkline>
    </v-sheet>

    <v-card-text class="pt-0">
      <div class="text-h6 font-weight-light mb-2 mt-4">
     Min: $ {{minValue}} -- Max: $ {{maxValue}}
      </div>
      <div class="subheading font-weight-light grey--text mt-4">
        Records obtained from <a href="https://apilayer.com/marketplace/currency_data-api">APILayer</a>
       
      </div>
      <v-divider class="my-2"></v-divider>
      <!-- <v-icon
        class="mr-2"
        small
      >
        mdi-clock
      </v-icon>
      <span class="text-caption grey--text font-weight-light">last registration 26 minutes ago</span> -->
    </v-card-text>
  </v-card>
    </div>
</template>
<script>
import axios from 'axios';
import {mapMutations} from 'vuex';
export default {
    name:"StatisticsComponent",
    data(){
        return{
          value: [
        
          ],
          currency:"USD",
          maxValue:null,
          minValue:null,
        }
    },
    methods:{
       ...mapMutations(['mostrarLoading','ocultarLoading']),
     async getdata(){
        let start = "2021-01-01";
        let end = "2022-01-01";
        let valores = null;
       
        // var myHeaders = new Headers();
        // myHeaders.append("apikey", "");
      
        var requestOptions = {
        method: 'GET',
        headers:{
            apikey: "Zdhodlsn42eF0Hpys2dqEQSEswXe9JEu"
        }
        };
        try{
          
          this.mostrarLoading({titulo:'Loading data'});
          let datos = await axios.get(`https://api.apilayer.com/currency_data/timeframe?start_date=${start}&end_date=${end}`,requestOptions);
          valores = Object.entries(datos.data.quotes); 
            console.log(valores);
          valores.forEach(element => {
              this.value.push(element[1]['USDUYU'])
          }
          );
          this.maxValue = Math.max(...this.value);
          this.minValue = Math.min(...this.value);
        }catch(error){
            //
        }finally{
           this.ocultarLoading()
        }
        }
    },
    mounted(){
     this.getdata();
    }


}
</script>