<template>
    <div>
        <div class="consulta__contenido">
            <h1 class="consulta__titulo">Pokedex Nacional</h1>
            <p class="consulta__instrucciones">
                Ingresa el nombre o el número de un pokemon para consultar.
            </p>
            <div class="consulta__formulario">
                <input type="text" class="formulario__info" v-model="pokeInput" >
                <button id="pokeSubmit" class="formulario__boton" @click="pokeRqst()">Consultar</button>
            </div>
        </div>
        <pokemon :objRqstd="pokeObj" :status="pokeStatus"></pokemon>
    </div>
</template>

<script>
import pokemon from './components/pokemon.vue';

export default {
  name: 'App',
  data() {
        return {
            pokeInput: '',
            pokeObj: {},
            pokeStatus: 'hidden',
        }
    },
    methods: {
        pokeRqst: function() {
            const pagRqst = async () => {
                this.pokeObj = {};
                try {
                    let urlApi = `https://pokeapi.co/api/v2/pokemon/${this.pokeInput}`;
                    this.pokeStatus = 'loading';
                    let res = await fetch(urlApi);
                    console.log(res);
                    if(res.status == 200) {
                        let toJson = await res.json();
                        this.pokeObj = toJson;
                        this.pokeStatus = 'ok';
                    } else {
                        this.pokeStatus = 'failed';
                    }
                } catch(err) {
                    console.log(err);
                }
            };
            pagRqst();
        }
    },
    components: {
        pokemon,
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
  margin-top: 60px;
}
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
body {
  font-family: 'Lato', sans-serif;
  color: darkslategray;
  background-color: #eeeeee;
}
.consulta, .respuesta {
  display: -webkit-flex;
  display: flex;
  justify-content: center;
  padding-top: 5vh;
}
.consulta__contenido{
  background-color: white;
  border-bottom: 2px solid darkslategrey;
  padding: 2.5% 10%;
  box-shadow: black;   
}
.consulta__titulo {
  font-size: 2rem;
  margin-bottom: 1rem;
  text-align: center;
}
.consulta__instrucciones {
  font-size: 1.25rem;
  margin-bottom: 1.5rem;
  text-align: center;
}
.consulta__formulario {
  display: -webkit-flex;
  display: flex;
  justify-content: center;
  width: 100%;
}
.consulta__formulario input{
  padding: 0 1rem;
  min-width: 25%;
  font-size: 1rem;
  margin: 0 5px;
  font-family: 'Lato', sans-serif;
  color: darkslategray;
}
.consulta__formulario button {
  padding: 1.25% 2.5%;
  font-size: 1rem;
  margin: 0 5px;
  font-family: 'Lato', sans-serif;
  color: darkslategray;
}

.invisible {
  display: none;
}
.visible {
  display: block;
}

.respuesta {
  flex-direction: column;
  padding: 0 5%;
  
}
.respuesta img {
  margin-right: 5vw;
  max-height: 150px;
}
.pokemon__card {
  background-color: #ffffff;
  border-radius: 5px;
  box-shadow: 2px 4px 4px #bcbcbc;
}
.respuesta__titulo{
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 5vw 0;
}
.respuesta__nombre{
  text-transform: capitalize;
}
.habilidad__texto, .movimiento__texto {
  width: 75vw;
}
.habilidad__texto h3, .habilidad__texto p {
  margin-bottom: 1rem;
}
.movimiento__texto h3, .movimiento__texto p {
  margin-bottom: 1rem;
}
.respuesta__habilidades_centrado, 
.respuesta__movimientos_centrado {
  display: flex;
  justify-content: center;
}
.respuesta__habilidades {
  margin-bottom: 5vw;
}
.respuesta__habilidades h2, .respuesta__movimientos h2{
  text-align: center;
  margin-bottom: 1.5rem;
}

</style>
