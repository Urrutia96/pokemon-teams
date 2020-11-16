<template>
  <div class="container mx-auto">
    
    <div class="grid grid-cols-2 gap-6">
      <!-- Pokemon List -->
      <div class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-5 gap-5 mt-6">
        <div draggable="true" @dragstart="drag(pokemon)" class="shadow hover:shadow-lg hover:bg-gray-100 p-2" v-for="pokemon in pokemons" :key="pokemon.entry_number">
          <div class="flex justify-center items-center">
            <img :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+(pokemon.entry_number)+'.png'" />
          </div>
          <div class="mt-2">
            <h1 class="text-center text-lg font-semibold capitalize">{{ pokemon.pokemon_species.name }}</h1>
          </div>
        </div>
      </div>
      <!-- End Pokemon List -->

      <!-- Teams -->
        <div>
          <div class="w-full h-56 border border-2" @dragover.prevent @drop.stop.prevent="addPokemon">
            <div v-for="one in teamOne" :key="one.entry_number">
              <div class="flex justify-center items-center">
                <img :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+(one.entry_number)+'.png'" />
              </div>
            </div>
          </div>
        </div>
      <!-- End Teams -->

    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios }){
    const pokedex = await $axios.$get('/pokedex/2')
    const pokemons = pokedex.pokemon_entries
    return {
      pokemons
    }
  },
  data(){
    return {
      dragItem: [],
      teamOne: [],
      teamTwo: []
    }
  },
  methods: {
    drag(pokemon){
      this.dragItem = pokemon
    },
    addPokemon(e){
      if(this.dragItem !== []){
        this.teamOne.push(this.dragItem)
        this.dragItem =[]
      }
    }
  }
}
</script>

<style>

</style>