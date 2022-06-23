<template>
  <v-app >
    <v-main>
      <v-container height="100%">
        <!-- BARRA DE CARGA -->
        <v-dialog
          v-model="loading.estado"
          hide-overlay
          persistent
          width="300">
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

    }
  },
  computed:{
    ...mapState(['loading'])
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
