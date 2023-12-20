<template>
  <div class="w-1/2 mx-auto my-20 shadow-xl bg-white rounded-lg" >
  <select v-model="selected">
    <option disabled value="">Escolha um item</option>
    <option>Frozen Drink</option>
    <option>Hot Drink</option>
    <option>Short Drink</option>
    <option>Long Drink</option>
  </select>
  <br>
  <span>Selecionado: {{ filteredDrinks }}</span>
  <!-- <button 
  class="bg-red-500 p-3 text-white"
  v-on:click="filteredDrinks()"
  > 
  Pesquisar
  </button> -->

  <!-- <ul v-for="drink in filteredDrinks" :key="drink.category">
  <li >
    {{ filteredDrinks }}
  </li>
</ul>
 </div> -->
 
</template>

<script lang="ts">
import Vue from 'vue'

interface Drink {
    id: number;
    name: string;
    category: string;
    description: string;
    image: string;
}

export default Vue.extend({
  data(){
    return {
      drink: {
      name: null,
      category:null,
      description:null,
      image:null,
      },
      selected: null,
      listDrinks: [],
    }
  },
  mounted(){
    this.generateListDrinks()
  },
  computed: {
    filteredDrinks() {
    let filterDrinks = [];
    filterDrinks = this.listDrinks.filter((filterDrink) => {
      if(this.selected === null){return filterDrink }
      return (
        filterDrink.category === this.selected
      )
    })
    const name = filterDrinks.map((i)=> i.name)
    return name
   }
  },
  methods: {
    async generateListDrinks(): Promise<void> {
     await this.$axios
      .$get("http://localhost:3333/api/drinks")
      .then((response) => {
       this.listDrinks = response.data;
      })
    },
  },
})
</script>
