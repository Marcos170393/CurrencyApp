<template>
  <v-app >
    <v-navigation-drawer app permanent color="blue" dark>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="text-h5">
            Currency App
          </v-list-item-title>
          <v-list-item-subtitle>
            Know Everything
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list
        dense
        nav
      >
      <router-link to="calendar"> 
        <v-list-item link>
          <v-list-item-icon>
           <v-icon>mdi-calendar-month</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>Calendar</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        </router-link>
        <router-link to="statistics">
        <v-list-item link>
          <v-list-item-icon>
            <v-icon>mdi-chart-bar</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>Statistics</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        </router-link>
      </v-list>
    </v-navigation-drawer>
    <v-main>
      <v-container height="100%">
        <!-- BARRA DE CARGA -->
        <v-dialog
          v-model="loading.estado"
          hide-overlay
          persistent
          width="300"
          >
         
          <v-card color="dark" dark>
            <v-card-text>
              {{loading.titulo}}
              <v-progress-linear
                indeterminate
                color="white"
                class="mb-0"
              ></v-progress-linear>
            </v-card-text>
          </v-card>
        </v-dialog>

      </v-container>

      
        
        <router-view/>
          
      
    </v-main>
  </v-app>
</template>
<script>
import {mapState} from 'vuex';

export default {
  name:'App',
  data(){
    return{
        items: [
          { title: 'Calendar', icon: '' },
          { title: 'Statistics', icon: '' },
          { title: 'About', icon: '' },
        ],
        right: null,
        
    }
  },
  computed:{
    ...mapState(['loading'])
  },
  components:{
   
  }
}
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body{
  width: 100%;
  height: 100%;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
