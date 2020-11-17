<template>
  <div>
    <Navbar />
    <div class="container mx-auto">
      
      <div class="grid grid-cols-1 gap-6" :class="{'md:grid-cols-2':user}">
        <!-- Pokemon List -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-5 mt-6">
          <div 
            draggable="true" 
            @dragstart="drag(pokemon.entry_number)" 
            class="shadow hover:shadow-lg hover:bg-gray-100 p-2" 
            v-for="pokemon in pokemons" 
            :key="pokemon.entry_number">
            <div class="flex justify-center items-center">
              <img :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+(pokemon.entry_number)+'.png'" />
            </div>
            <div class="mt-2">
              <h1 class="text-center text-lg font-semibold capitalize">{{ pokemon.pokemon_species.name }}</h1>
              <div class="grid grid-cols-2 gap-4 text-white" v-if="user">
                <button @click="buttomPokemon(pokemon.entry_number,'teamOne')" class="px-2 py-2 bg-red-600 text-sm">+ Team One</button>
                <button @click="buttomPokemon(pokemon.entry_number,'teamTwo')" class="px-2 py-2 bg-blue-600 text-sm">+ Team Two</button>
              </div>
            </div>
          </div>
        </div>
        <!-- End Pokemon List -->

        <!-- Teams -->
          <div class="relative py-10 hidden md:block" v-show="user">
            <div class="sticky top-0">

              <div class="grid grid-cols-2 gap-4">
                <div>
                  <div class="text-red-600 text-xl font-bold mt-10">Team One</div>
                  <div class="w-full h-32 border" @dragover.prevent @drop.stop.prevent="addPokemon('teamOne')">
                    <div class="flex flex-col justify-center items-center h-full">
                      <!-- Feather Icon: upload-cloud -->
                      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-upload-cloud"><polyline points="16 16 12 12 8 16"></polyline><line x1="12" y1="12" x2="12" y2="21"></line><path d="M20.39 18.39A5 5 0 0 0 18 9h-1.26A8 8 0 1 0 3 16.3"></path><polyline points="16 16 12 12 8 16"></polyline></svg>
                      <span>Arrastra aqui</span>
                    </div>
                  </div>
                  <div class="grid grid-cols-2">
                    <div class="flex justify-center items-center p-2 border" v-for="(item, index) in teamOne" :key="'teamOne'+index">
                      <img :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+(item)+'.png'" />
                      <button @click="deletePokemon(index, 'teamOne')" class="focus:outline-none">
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-trash-2"><polyline points="3 6 5 6 21 6"></polyline><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path><line x1="10" y1="11" x2="10" y2="17"></line><line x1="14" y1="11" x2="14" y2="17"></line></svg>
                      </button>
                    </div>
                  </div>
                </div>
                <div>
                  <div class="text-blue-600 text-xl font-bold mt-10">Team Two</div>
                  <div class="w-full h-32 border" @dragover.prevent @drop.stop.prevent="addPokemon('teamTwo')">
                    <!-- <div v-for="(item, index) in teamTwo" :key="'teamTwo'+index"> -->
                    <div class="flex flex-col justify-center items-center h-full">
                      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-upload-cloud"><polyline points="16 16 12 12 8 16"></polyline><line x1="12" y1="12" x2="12" y2="21"></line><path d="M20.39 18.39A5 5 0 0 0 18 9h-1.26A8 8 0 1 0 3 16.3"></path><polyline points="16 16 12 12 8 16"></polyline></svg>
                      <span>Arrastra aqui</span>
                    </div>
                  </div>
                  <div class="grid grid-cols-2">
                    <div class="flex justify-center items-center p-2 border " v-for="(item, index) in teamTwo" :key="'teamOne'+index">
                      <img :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+(item)+'.png'" />
                      <button @click="deletePokemon(index, 'teamTwo')" class="focus:outline-none">
                        <!-- Feather Icon: trash-2 -->
                        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-trash-2"><polyline points="3 6 5 6 21 6"></polyline><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path><line x1="10" y1="11" x2="10" y2="17"></line><line x1="14" y1="11" x2="14" y2="17"></line></svg>
                      </button>
                    </div>
                  </div>
                </div>
              </div>

            </div>
          </div>
        <!-- End Teams -->

      </div>
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
      user: [],
      dragItem: 0,
      teamOne: [],
      teamTwo: []
    }
  },
  methods: {
    drag(pokemon){
      this.dragItem = pokemon
    },
    buttomPokemon(pokemon, team){
      this.dragItem = pokemon 
      this.addPokemon(team);
    },
    addPokemon(team){
      if(this.dragItem > 0){
        if(team == 'teamOne'){
          if(this.canAddPokemon(team)){
            this.teamOne.push(this.dragItem)
            localStorage.setItem('teamOne', JSON.stringify(this.teamOne))
          }
        }else{
          if(this.canAddPokemon(team)){
            this.teamTwo.push(this.dragItem)
            localStorage.setItem('teamTwo', JSON.stringify(this.teamTwo))
          }
        }
        this.dragItem = 0
      }
    },
    canAddPokemon(team){
      const tempTeam = team == 'teamOne' ? this.teamOne : this.teamTwo
      // Check if pokemons are 5
      if(Object.keys(tempTeam).length > 5){
        return false
      }

      // check for duplicated
      const duplicated = tempTeam.every((e, i, a) => a.indexOf(e) === i)
      let repeat = 0;

      // Check if new entry are repeat
      tempTeam.forEach(element => {
        if(element === this.dragItem){
          repeat++;
        }
      });
      
      if(!duplicated && repeat>0){
        return false 
      }

      return true;
    },
    deletePokemon(index, team){
      if(team == 'teamOne'){
        localStorage.removeItem('teamOne')
        this.teamOne.splice(index, 1)
        localStorage.setItem('teamOne', JSON.stringify(this.teamOne))
      }else{
        localStorage.removeItem('teamTwo')
        this.teamTwo.splice(index, 1)
        localStorage.setItem('teamTwo', JSON.stringify(this.teamTwo))
      }
    }
  },
  mounted() {
    this.user = JSON.parse(localStorage.getItem('user'))
    this.teamOne = localStorage.getItem('teamOne') === null ? [] : JSON.parse(localStorage.getItem('teamOne'))
    this.teamTwo = localStorage.getItem('teamTwo') === null ? [] : JSON.parse(localStorage.getItem('teamTwo'))
  }
}
</script>

<style>

</style>