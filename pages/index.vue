<template>
  
</template>

<script>
export default {
  async asyncData({ $axios }){
    const generation = await $axios.$get('/generation/1')
    const pokemons = generation.pokemon_species
    return {
      pokemons
    }
  }
}
</script>

<style>

</style>