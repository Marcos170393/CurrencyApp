<template>
    <div>
        
    </div>
</template>
<script>
import axios from 'axios';
import {mapMutations} from 'vuex';
export default {
    name:"StatisticsComponent",
    data(){
        return{
        }
    },
    methods:{
        ...mapMutations(['mostrarLoading','ocultarLoading']),
      async  getdata(){
             console.log(this.currency);
               this.mostrarLoading({titulo:'Loading data'});
            await axios.get(`http://www.ine.gub.uy/c/document_library/get_file?uuid=1dcbe20a-153b-4caf-84a7-7a030d109471`)
        }
    }


}
</script>