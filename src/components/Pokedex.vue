<template>
  <div class="container">
    <div class="pokedex-container">
      Aqui van los demas componentes
      <PokemonInformation/>
      <!-- <div class="row">
          <div class="col-sm-2">
              <span class="pokemon-number">#001</span>
              <h3 class="pokemon-name">Bulbasaur </h3>
              <div class="pokemon-type">
                <b>Planta </b><b> Veneno</b><br/>
              </div>
          </div>
      </div> -->
      <!-- <div class="row">
            <div class="col-sm-4">
              <img class="pokemon-image" src="https://img.pokemondb.net/artwork/bulbasaur.jpg" alt="Smiley face"><br/>
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
                    <td>xx</td>
                    <td>xx</td>
                    <td>xx/xx</td>
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
                  <tr>
                    <td>xx</td>
                    <td>Lorem ipsum dolor sit, amet consectetur adipisicing elit.</td>
                  </tr>
                  <tr>
                    <td>xx</td>
                    <td>Lorem ipsum dolor sit, amet consectetur adipisicing elit.</td>
                  </tr>
                </tbody>
              </table>
              <img class="pokemon-sprite" src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/4.png">
              <img class="pokemon-sprite" src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/shiny/4.png">
              <img class="pokemon-sprite" src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/4.png" >
              <img class="pokemon-sprite" src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/shiny/4.png">
              <!-- <b>EVOLVES:</b><br/><br/> -->
              <!-- <br/>
              <img class="pokemon-evolution" src="https://img.pokemondb.net/artwork/ivysaur.jpg"> &nbsp&nbsp <font-awesome-icon icon="arrow-right" /> &nbsp&nbsp<img class="pokemon-evolution" src="https://img.pokemondb.net/artwork/venusaur.jpg">
            </div>
            <div class=" col-sm-2 offset-sm-1 card h-25 pokemon-stats">
              <div class="card-body ">
                <b>Hp: 12</b><br/>
                <b>Atack: 10</b><br/>
                <b>Def: 12</b><br/>
                <b>Speed: 12</b><br/>
                <b>Sp.Atack: 12</b><br/>
                <b>Sp.Def: 12</b><br/>
              </div>
            </div>
            <div class="col-sm-4 offset-sm-1">
              <div class="card ">
                <div class="card-body h-25">
                  <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Ipsam magni velit perspiciatis quae quos officiis accusamus, consequuntur veniam dolorem animi, vitae quia facilis doloremque ullam facere autem, accusantium tempora praesentium.</p>
                  <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Ipsam magni velit perspiciatis quae quos officiis accusamus, consequuntur veniam dolorem animi, vitae quia facilis doloremque ullam facere autem, accusantium tempora praesentium.</p>
                </div>
              </div>
              <img src="https://image.flaticon.com/icons/svg/1377/1377975.svg" alt="English language" class="replaced-svg languaje-icon" >
              <img src="https://image.flaticon.com/icons/svg/1377/1377973.svg" alt="Spanish language" class="replaced-svg languaje-icon" >
              <img src="https://image.flaticon.com/icons/svg/206/206789.svg" alt="Japanish language" class="replaced-svg languaje-icon" >
            </div> -->
      </div>
      <!-- <div class="row justify-content-md-center">
         <button class="page-link" href="#" aria-label="Previous"><font-awesome-icon icon="angle-double-left" /></button> &nbsp <input type="text" placeholder="Find Pokemon">&nbsp<button  class="page-link" href="#" aria-label="Next"><font-awesome-icon icon="angle-double-right" /></button>
      </div> -->
    </div>
</template>

<script>
import PokemonInformation from './PokemonInformation.vue';

export default {
  name: 'Pokedex',
  data() {
    return {
    };
  },
  components: {
    PokemonInformation,
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
