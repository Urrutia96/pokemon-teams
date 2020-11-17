<template>
  <div>
    <Navbar />
    <div class="w-full  flex justify-center items-center" v-if="user">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <div>
          <div class="text-red-800 text-xl font-bold mt-10">Team One</div>
          <div class="mt-5 grid grid-cols-2">
            <div class="flex justify-center items-center p-2 border" v-for="(item, index) in teamOne" :key="'teamOne'+index">
              <img :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+(item)+'.png'" />
              <button @click="deletePokemon(index, 'teamOne')" class="focus:outline-none">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-trash-2"><polyline points="3 6 5 6 21 6"></polyline><path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path><line x1="10" y1="11" x2="10" y2="17"></line><line x1="14" y1="11" x2="14" y2="17"></line></svg>
              </button>
            </div>
          </div>
        </div>
        <div>
          <div class="text-red-800 text-xl font-bold mt-10">Team Two</div>
          <div class="mt-5 grid grid-cols-2">
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
</template>

<script>
export default {
  data(){
    return {
      user: [],
      teamOne: [],
      teamTwo: []
    }
  },
  methods: {
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