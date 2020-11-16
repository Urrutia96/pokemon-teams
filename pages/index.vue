<template>
  <div class="container mx-auto">
    
    <div class="grid grid-cols-2 gap-6">
      <!-- Pokemon List -->
      <div class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-5 gap-5 mt-6">
        <div 
          draggable="true" 
          @dragstart="drag(pokemon)" 
          class="shadow hover:shadow-lg hover:bg-gray-100 p-2" 
          v-for="pokemon in pokemons" 
          :key="pokemon.entry_number">
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
        <div class="relative py-10">
          <div class="sticky top-0">

            <div class="grid grid-cols-2 gap-4">
              <div>
                <div class="text-red-800 text-xl font-bold mt-10">Team One</div>
                <div class="w-full h-32 border" @dragover.prevent @drop.stop.prevent="addPokemon('teamOne')">
                  <div class="flex flex-col justify-center items-center h-full">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-upload-cloud"><polyline points="16 16 12 12 8 16"></polyline><line x1="12" y1="12" x2="12" y2="21"></line><path d="M20.39 18.39A5 5 0 0 0 18 9h-1.26A8 8 0 1 0 3 16.3"></path><polyline points="16 16 12 12 8 16"></polyline></svg>
                    <span>Arrastra aqui</span>
                  </div>
                </div>
                <div class="" v-for="(item, index) in teamOne" :key="'teamOne'+index">
                  <img :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+(item.entry_number)+'.png'" />
                </div>
              </div>
              <div>
                <div class="text-red-800 text-xl font-bold mt-10">Team Two</div>
                <div class="w-full h-32 border" @dragover.prevent @drop.stop.prevent="addPokemon('teamTwo')">
                  <!-- <div v-for="(item, index) in teamTwo" :key="'teamTwo'+index"> -->
                  <div class="flex flex-col justify-center items-center h-full">
                    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-upload-cloud"><polyline points="16 16 12 12 8 16"></polyline><line x1="12" y1="12" x2="12" y2="21"></line><path d="M20.39 18.39A5 5 0 0 0 18 9h-1.26A8 8 0 1 0 3 16.3"></path><polyline points="16 16 12 12 8 16"></polyline></svg>
                    <span>Arrastra aqui</span>
                  </div>
                </div>
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
    addPokemon(team){
      if(Object.keys(this.dragItem).length){
        if(team == 'teamOne'){
          if(this.canAddPokemon(team)){
            this.teamOne.push(this.dragItem)
          }
        }else{
          if(this.canAddPokemon(team)){
            this.teamTwo.push(this.dragItem)
          }
        }
        this.dragItem =[]
      }
    },
    canAddPokemon(team){
      const tempTeam = team == 'teamOne' ? this.teamOne : this.teamTwo
      if(Object.keys(tempTeam).length > 5){
        return false
      }

      let repeat = 0;
      tempTeam.forEach(element => {
        if(element === this.dragItem){
          repeat++;
        }
      });

      if(repeat>=2){
        return false 
      }
      return true;
    }
  }
}
</script>

<style>

</style>