<template>
    <div>
      <div class="row">
        <div class="col-sm-2">
          <span class="pokemon-number" v-if="pokemon.id < 10">#{{ '00'+ pokemon.id }}</span>
          <span class="pokemon-number" v-else-if="pokemon.id > 10 && pokemon.id < 100">#{{ '0'+ pokemon.id }}</span>
          <span class="pokemon-number" v-else>#{{ pokemon.id }}</span>
          <!-- <h3 class="pokemon-name">Bulbasaur </h3> -->
          <button @click="incrementId">clickme</button>
          <h3 class="pokemon-name">{{ pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1) }} </h3>
          <div class="pokemon-type">
            <b v-for="(type,index) in pokemon.types" :key="pokemon.index"> {{ type.name.charAt(0).toUpperCase() + type.name.slice(1) }}</b>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-sm-4">
          <img class="pokemon-image" :src="pokemon.image" alt="pokemon image"><br/>
          <img class="pokemon-sprite" v-for="value in pokemon.sprites" :key="pokemon.index" v-if ="value" :src= "value">
          <table class="table pokemon-table">
                <thead>
                  <tr>
                    <th>Weight</th>
                    <th>Height</th>
                    <th>Type</th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <td>{{ pokemon.height }} m</td>
                    <td>{{ pokemon.weight}} Kg</td>
                    <td v-for="(type,index) in pokemon.types" :key="pokemon.index">{{ type.name.charAt(0).toUpperCase() + type.name.slice(1) }}</td>
                  </tr>
                </tbody>
              </table>
              <table class="table pokemon-table">
                <thead>
                  <tr>
                    <th>Abilities</th>
                    <th>Description</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(ability,index) in pokemon.abilities" :key="pokemon.index">
                    <!-- <td>xx</td> -->
                    <td >{{ ability.charAt(0).toUpperCase() + ability.slice(1) }}</td>
                    <td> {{ pokemon.abilityDescription[index] }}</td>
                  </tr>
                </tbody>
              </table>
              <b>EVOLVES:</b><br/>
              <!-- Añadir la funcion de clickar para mostrar el pokemon... -->
              <template>
                <div v-for="(evolve,index) in pokemon.evolves" :key="index" style="display:inline-block;">
                  <img class="pokemon-evolution" v-if="evolve" :src= "'https://img.pokemondb.net/artwork/' + evolve.name + '.jpg'">
                  &nbsp&nbsp <font-awesome-icon icon="arrow-right" v-if="index + 1 < pokemon.evolves.length"/> &nbsp&nbsp
                </div>
              </template>
        </div>
         <div class=" col-sm-3 offset-sm-1 card h-25 pokemon-stats">
            <div class="card-body" >
              <b v-for="(stat, index) in pokemon.stats" :key="index">
                {{ stat.statName.charAt(0).toUpperCase() + stat.statName.slice(1) }}: {{ stat.statValue}} <br/><br/>
              </b>
            </div>
          </div>
          <div class="col-sm-3 offset-sm-1">
            <div class="card ">
              <div class="card-body h-25">
                <p >{{ pokemon.description[0].description }}</p> 
              </div>
            </div>
            <button @click="incrementId">clickme</button>
            <img @click="changeLanguageDescription('ja')" src="https://image.flaticon.com/icons/svg/206/206789.svg" alt="Japanish language" class="replaced-svg languaje-icon" >
            <img @click="changeLanguageDescription('en')" src="https://image.flaticon.com/icons/svg/1377/1377975.svg" alt="English language" class="replaced-svg languaje-icon" >
            <img @click="changeLanguageDescription('es')" src="https://image.flaticon.com/icons/svg/1377/1377973.svg" alt="Spanish language" class="replaced-svg languaje-icon" >
            <!-- <img @click="changeLanguageDescription('red-version')" src="../assets/red_version.png" alt="Red Version" > -->
            <!-- <img src="./assets/logo.png"> -->
          </div>
    </div>
    <!-- <div class="row justify-content-md-center">
      <button @click="decrementId" class="page-link" href="#" aria-label="Previous"><font-awesome-icon icon="angle-double-left" /></button> &nbsp <input type="text" placeholder="Find Pokemon">&nbsp<button @click="incrementId" class="page-link" href="#" aria-label="Next"><font-awesome-icon icon="angle-double-right" /></button>
    </div> -->
  </div>
</template>

<script>
import lastPokemon from '../constants.js';

const axios = require('axios');
let language = 'en'
let version = 'red'
//falta filtrar la descripcion por juegos e idiomas...
export default {
  name: 'pokemonInformation',
  data() {
    return {
      pokemon: {
        id: 1,
        name: '',
        image: '',
        weight: '',
        height: '',
        stats: [],
        types: [],
        abilities: [],
        abilityDescription: [],
        sprites: {},
        evolves: [],
        description: [],
      },
    };
  },
  methods: {
    changeLanguageDescription(newLanguage){
      language = newLanguage;
      this.pokemon.description = []
      this.getPokemonDescription(this.pokemon.id, language)
    },
    // funcion para obtener la informacion completa del pokemon
    async getPokemonInfo(id) {
      await axios.get(`https://pokeapi.co/api/v2/pokemon/${id}`)
        .then((response) => {
          console.log(response.data);
          const pokemonData = response.data;
          this.pokemon.name = pokemonData.name;
          this.getPokemonImage(this.pokemon.name);
          this.pokemon.weight = pokemonData.weight / 10;
          this.pokemon.height = pokemonData.height / 10;
          for (const i in pokemonData.stats) {
            const stat = pokemonData.stats[i];
            this.pokemon.stats.push({'statName': stat.stat['name'], 'statValue': stat.base_stat})
          }
          for (const i in pokemonData.types) {
            const tipo = response.data.types[i];
            this.pokemon.types.push(tipo.type);
          }
          for (const i in pokemonData.abilities) {
            const ability = response.data.abilities[i];
            this.pokemon.abilities.push(ability.ability.name);
            this.getAbilityDescription(ability.ability.url);
          }
          this.pokemon.sprites = pokemonData.sprites;
          this.getEvolves(id);
          this.getPokemonDescription(id, language);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    // fuincion para obtener la imagen del pokemon
    getPokemonImage(pokemonName) {
      this.pokemon.image = `https://img.pokemondb.net/artwork/${pokemonName}.jpg`;
    },
    // funcion para obtener las evoluciones que tenga el pokemon
    async getEvolves(pokemonId) {
      console.log(pokemonId)
      await axios.get(`https://pokeapi.co/api/v2/evolution-chain/${pokemonId}`)
        .then((response) => {
          if (response.data.chain.evolves_to.length > 0) {
            this.addEvolution(response.data.chain.evolves_to[0]);
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
    // funcion recursiva para obtener las posibles evoluciones del pokemon
    addEvolution(evolveInformation) {
      this.pokemon.evolves.push({
        name: evolveInformation.species.name,
        id: evolveInformation.species.url.slice(-2, -1),
      });
      if (evolveInformation.evolves_to.length > 0) {
        this.addEvolution(evolveInformation.evolves_to[0]);
      }
    },
    // funcion para obtener las descripcion de las habilidades que posea el pokemon
    async getAbilityDescription(url) {
      await axios.get(url)
        .then((response) => {
          const descriptionData = response.data;
          this.pokemon.abilityDescription.push(descriptionData.effect_entries[0].effect);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    async getPokemonDescription(pokemonId, language){
      //pokemon-species/1/
      await axios.get('https://pokeapi.co/api/v2/pokemon-species/'+pokemonId.toString())
      .then((response) => {
        for (let i = 0; i < response.data.flavor_text_entries.length; i++) {
          const languageDescription = response.data.flavor_text_entries[i];
          //eng
          // console.log(languageDescription)
          if(languageDescription.language.name === language ){
            this.pokemon.description.push({
              'language': languageDescription.language.name ,
              'version': languageDescription.version.name,
              'description': languageDescription.flavor_text
            })
            console.log('encontro el idioma..')
            // console.log(this.pokemon.description)
          }
          
        }
        // for (const i in response.data.flavor_text_entries.length) {
        //     const desc = response.data.flavor_text_entries[i];
        //     console.log(desc)
        //   }
      })
      .catch((error) => {
        console.log(error)
      });
    },
    // incrementa el identificador del pokemon (para cuando le de a la flecha derecha a en el inferior de la pantalla)
    incrementId() {
      this.pokemon.id === lastPokemon ? this.pokemon.id = 1 : this.pokemon.id += 1;
      this.getPokemonInfo(this.pokemon.id);
      this.pokemon.types = [];
      this.pokemon.stats = [];
      this.pokemon.abilities = [];
      this.pokemon.abilityDescription = [];
      this.pokemon.evolves = [];
    },
    // incrementa el identificador del pokemon (para cuando le de a la flecha izquierda a en el inferior de la pantalla)
    decrementId() {
      this.pokemon.id === 1 ? this.pokemon.id = lastPokemon : this.pokemon.id -= 1;
      this.getPokemonInfo(this.pokemon.id);
      this.pokemon.stats = [];
      this.pokemon.types = [];
      this.pokemon.abilities = [];
      this.pokemon.abilityDescription = [];
      this.pokemon.evolves = [];
    },
  },
  created() {
    this.getPokemonInfo(this.pokemon.id);
  },
};
</script>

<style>
.pokemon-number{
  margin-left: -120px;
}
.pokemon-name{
  margin-left: -30px;
}
.pokemon-type{
  margin-left: -40px;
}
.pokemon-image{
    width:100px;
    height: 100px;
}
.pokemon-table{
  margin-top:10px;
}
.pokemon-info{
  margin-top: 25px;
}
.pokemon-sprite{
  margin-top: 10px;
  width:80px;
  height: 80px;
}
.pokemon-stats{
    margin-top: 75px;
}
.pokemon-evolution{
  margin-top: 20px;
  border-radius: 50%;
  /* border: 1px solid black; */
  width:80px;
  height: 60px;
}
.languaje-icon{
  margin-top:10px;
  padding-left: 10px;
  width:30px;
  height: 30px;
}
::-webkit-input-placeholder {
   color: #808080;
   text-align: center;
}
</style>
