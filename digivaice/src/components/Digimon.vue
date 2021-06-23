<template>
    <div class="card mb-6">
            <div class="card-image" >
                <figure id="figure" class="image is-128x128 ">
                    <img :src="image[num]" alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <h3 class="title is-4">{{name}}</h3>
                        <h4 class="subtitle is-6">Level: {{nivel[num]}}</h4>
                    </div>
                </div>

                <div class="content">
                </div>
            </div>
        </div>

</template>

<script>
  import axios from 'axios'

    export default {
        props: {
            name: String,
            num: Number

        },

        created () {
            axios.get("https://digimon-api.vercel.app/api/digimon").then(res => {

                this.digimons = res.data

                this.digimons.forEach(digimon => {
                    this.nivel.push(digimon.level) // Array com nivel dos Digimons
                    this.image.push(digimon.img)    // Array com imagem dos digimons
                })

            
            }).catch(error => {console.log(error)})

        },

        data() {
            return {
                
                nivel: [],
                image: [] ,
                digimons: []

                
            }
        }
      
    }

</script>

<style>
    #figure {
        margin-left: 36%;
    }
</style>