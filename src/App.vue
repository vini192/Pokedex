<template >

<div class="mainxmain"> 
  <div class="mainxheader" >

      <div class="headerxlogo"> <!-- LOGO C:\Users\ViniciusF\Desktop\pokedex\src\assets\poke-logo.png-->
        <img src="./assets/poke-logo.png" >
      </div>

      <div class="headerxmenu">
          <div> 
            <ul>
              <li><a href="#" class="menuli">Inicio</a></li>
              <li><a href="#" class="menuli">Sobre</a></li>
              <li><a href="#" class="menuli">Contato</a></li>
            </ul>
          </div>

          <div class="search-box">
            <input class="search-txt" type="text" v-model="search" placeholder="Buscar Pokemon">  
            <a class="search-btn" href="#" style="margin-top: -37px">
              <img src="./assets/loupe.png">
            </a>
          </div>
      </div>
  </div>


  <div class="hoverlist"  v-bind:style="tamanho">
    <div class="mainxnavxleft"  v-on:click="NavLeft">
        <img src="./assets/back.png">
    </div>

    <div class="mainxnavxright" v-on:click="NavRight">
        <img src="./assets/next.png">
    </div>


    <div class="corpoxlistapokemons"> 
      <h1>1º Geração</h1>
        <div class="corpoxlista" v-bind:style="'margin-left:' + ScrollX + 'px' "> 
          <div v-for="(poke, index) in resultadoBusca" :key="index" >
            <div class="PokeLeft">
            <Pokemon  :name="poke.name"  :url="poke.url" :num="index+1"/>
            </div>
          </div>
        </div>
    </div>
  </div>
</div> 

</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon';
//import func from '../vue-temp/vue-editor-bridge';

export default {
  name: 'App',

  data() {
    return {
    pokemons: [],
    testes: [],
    tamanho: '',
    search: '',
    ScrollX: 0,
    }
  },


  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then( res =>{
      this.testes = res
      //console.log(res)
      this.pokemons = res.data.results
      this.tamanho = "width: " + this.pokemons.length * 170 + "px"
      console.log(this.tamanho)
    })
  },

  components: {
      Pokemon
  },

  methods: {
    NavLeft: function() {
    if(this.ScrollX != 0){
     this.ScrollX = this.ScrollX + 450
    }
    },
    NavRight: function() {
    if(this.ScrollX != -21150)
      this.ScrollX = this.ScrollX - 450
    }
  },

  computed: {
    resultadoBusca: function(){
      if(this.search == '' || this.search == ' '){
        return this.pokemons
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.search)
      }
    }
  }



  
 
}
</script>

<style>
/*  <div v-for="(poke, index) in pokemons" :key="index">
            <Pokemon  :name="poke.name"  :url="poke.url" :num="index+1"/>
        </div> 
#app {
  font-family: 'Roboto', sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: black;
}        
        
        
*/
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap');

*{
  font-family: 'Roboto', sans-serif;
  margin: 0;
}
.mainxmain {
  margin:0;
  background-color:white;

  

}

.mainxheader{
  height: 100px;
  display: flex;
  flex-direction: row;
  background-color: red;
}

/* HEADER MENUU  */
.headerxmenu{
  position: absolute;
  right: 30%;
}

.headerxmenu ul{
  list-style-type: none;
  margin: 0;
  padding: 0;
  
}

.headerxmenu li {
  float: left;
  margin: 20px 50px 0 0;
  bottom: 0;
  padding: 10px;

}

.headerxmenu li a{
  display: inline-block;
  color: white;
  text-align: center;
  margin:0px auto;
  text-transform: uppercase;
  font-size: 25px;
}  

.menuli::after{
  content: '';
  display: block;
  width: 0;
  height: 2px;
  background: white;
  transition: width .3s;
}
.menuli:hover::after{
  width: 100%;
  transition: width .3s;
}



/* HEADER MENUU  */

.headerxlogo {
  margin-left: 1%;
  width: 12%;
}



/*  */

.corpoxlistapokemons{


}

.corpoxlista {
  

}


.corpoxlistapokemons h1{
  font-size: 25px;
  margin: 0px 0px 0px 50px;
}


.mainxnavxleft {
  left: 0;

}
.mainxnavxright {
  right: 0;
}

.mainxnavxright,
.mainxnavxleft{
  position: absolute;
  width: 40px;
  height: 260px;
  background-color: rgb(132, 137, 146, 0.7);
  z-index: 99;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: all ease 0.3s;
}


.hoverlist:hover .mainxnavxright,
.hoverlist:hover .mainxnavxleft{
  opacity: 1;
}

.PokeLeft {
  margin-left: 40px;
}



.search-box{
  position: absolute;
  top: 50%;
  left: 150%;
  transform: translate(-50%,-50%);
  /*background: #2f2f2f;*/
  background: white;
  height: 50px;
  border-radius: 40px;
  padding: 10px;
  border: solid 1px black;
}

.search-btn {
display: flex;
float: right;
color: #0080ff;
width: 40px;
height: 40px;
border-radius: 50%;
background: #ffffff;


}

.search-txt{
  border: none;
  background: none;
  outline: none;
  float: left;
  color: black;
  font-size: 16px;
  transition: 0.4s;
  line-height: 30px;
  width: 0px;
}



.search-box:hover > .search-txt{
 width: 240px;
 padding: 0 6px;
}


</style>
