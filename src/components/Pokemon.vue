<template>
    <div id="Pokemon">
        

    <div class="pokemonxfoto">
        <img :src="CurrentImg" alt="Placeholder image">
    </div>

    <div class="pokemonxname">
        <div>
        <h3> {{PrimeiraMaiscula(name)}} </h3>
        </div>
     

       <div v-for="(tipos, index) in types" :key="index">
           <div class="tamanhoImagem"> 
            <img v-bind:src="require('../assets/' + tipos.type.name + '.png')"/>


           </div>
        </div>   
    
    </div>
            
      
    </div>
    
</template>

<script>
import axios from 'axios';
//import func from '../../vue-temp/vue-editor-bridge';

export default {
    created:function (){ 
        axios.get(this.url).then( res =>{

       // this.pokemon.type = res.data.types[0].type.name;
        //this.pokemon.type = res.data.types;

        this.pokemon.front = res.data.sprites.front_default;
        this.pokemon.back = res.data.sprites.back_default;
        this.CurrentImg = this.pokemon.front
        this.types = res.data.types;
       
    
        })
    },
    data(){
        return {
            isFront: true,
            a: 3,
            CurrentImg: '',
            pokemon: {
                types: '',
                front: '',
                back: '',


            },
            
            types: [],
            CaminhoIcone: '',
        }
    },
    props: {
        num: Number,
        name: String, 
        url: String
    },

    methods: {
        PrimeiraMaiscula: function(value){
            var novoNome = value[0].toUpperCase() + value.slice(1);
            return novoNome
        },

        MudarFoto: function(){
            if(this.isFront){
                this.isFront = false
                this.CurrentImg = this.pokemon.back
            }else{
                this.isFront = true
                this.CurrentImg = this.pokemon.front
            }
        },

        IconePokemon: function(value){
            if (value){
                this.CaminhoIcone = '../assets/' + value + '.png'
            }

        }
    }
}
</script>

<style scoped>


@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap');

*{
  font-family: 'Roboto', sans-serif;
  margin: 0;
}

#Pokemon{
    margin-left: 2px;
    padding: 20px;
    width: 150px;
    float: left;
    border-radius: 50px;
    background-color: rgba(243, 209, 16, 0.5);
    text-align: center;
    align-items: center;
    justify-content: center;
    
    
}

.pokemonxfoto {
    border-radius: 50px;
    background-color: white;
}

.pokemonxfoto img{
    width: 100%;
    transform: scale(0.9);
    transition: all ease 0.3s;
    cursor: pointer;
}
.pokemonxfoto img:hover{
    transform: scale(1.5);
}

.pokemonxname {
    font-size: 20px;
    text-align: center;
    align-items: center;
    justify-content: center;
}

.tamanhoImagem {
    width: 40px;
    margin-left: 10px;
    padding: 1px;
    float: left;
}
</style>