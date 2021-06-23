<template>
  <div id="app" class="container">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/logo.png" class="mb-6" id="logo" alt="">
      <div id="form is-offset-one-quarter">
        <input v-model="search" class="input is-rounded mb-2" placeholder="Pesquise um digimon, ex: Garurumon" type="text" disabled>
        <button @click="searchDigimon()" class="button is-primary is-small is-fullwidth mb-6">Pesquisar</button>
      </div>
      <div v-for="(digimon, num) in filteredDigimons" :key="digimon" >
              <Digimon :name="digimon" :num="num"/>

      </div>
      
    </div>
    
  </div>
</template>

<script>
  import axios from 'axios'
  import Digimon from './components/Digimon.vue'



  export default {
    name: 'App',

    components: {
      Digimon
    },

    data() {
      return {
        digimonsData: [],
        digimonsInfo: [],
        filteredDigimons: [],
        numberDigimon:[], // Array que irá capturar index do digimon na função searchDigimon, 
                          // a fim de poder posteriormente aplicar um filtro de pesquisa
        Name:[],
        search: ""
      }
    },

    created () {
      axios.get("https://digimon-api.vercel.app/api/digimon").then(res => {
        this.digimonsData = res.data
        
        this.digimonsData.forEach(digimon => {
          this.Name.push(digimon.name) // Nome dos digimons
        })
        this.digimonsInfo.push(this.Name)
        

        this.filteredDigimons = this.digimonsInfo[0] // Array responsável por filtrar busca por nome do Digimon


      }).catch(error => {console.log(error)})
    }, 

    methods: {
      searchDigimon() { //Pesquisar um digimon pelo nome


        if (this.search.trim() == '') {
          alert("Informe o nome de um Digimon!")
          this.filteredDigimons = this.digimonsInfo[0]

        } else {

          this.filteredDigimons = this.digimonsInfo[0]
          this.filteredDigimons = this.digimonsInfo[0].filter(digi => this.search == digi)

         /* this.filteredDigimons.forEach((digimon, index) =>{

          
          if (digimon == this.search) {
            console.log(index)
            console.log(digimon)
          
          } */
            

        }



      }
    }

  }


</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
    padding-top: 40px;

}

body {
  background-color: rgb(94, 54, 94);
  height: 100%;
}

#logo {width: 300px;}

</style>

