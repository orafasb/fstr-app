<template>
  <div class="w-1/2 mx-auto my-20 text-center	shadow-xl rounded-lg bg-white-500 shadow-lg shadow-purple-500/50" >
    <h1 class="font-mono text-3xl my-5 ">Make your Drink</h1>
    <p class="font-mono ">Busque uma bebida</p>
  <input v-model="search" placeholder="Digite uma bebida" class="w-1/2 h-10 mx-auto  my-5  shadow-xl font-mono rounded bg-gray-300 px-4 font-semibold shadow-purple-380/50 hover:bg-gray-100 outline-none active:outline-none focus:outline-none">
  </input>
    <p class="font-mono ">Ou escolha uma categoria</p>
  <select v-model="selected"  class="w-1/2 h-10 mx-auto my-2 shadow-xl font-mono  rounded bg-gray-300 px-4 font-semibold shadow-purple-380/50 hover:bg-gray-100 outline-none active:outline-none focus:outline-none">
    <option disabled value="" >Escolha um item</option>
    <option>Frozen Drink</option>
    <option>Hot Drink</option>
    <option>Short Drink</option>
    <option>Long Drink</option>
  </select>
  <p class="my-5"></p>
  <tr class="bg-gray-100 h-10 mx-auto my-auto " v-for="filteredDrink in filteredDrinks" v-bind:key='filteredDrink.id'>
    <td class="w-1/5 content-center font-mono "><button @click="toggleModal = !toggleModal && filteredDrink ">{{filteredDrink.name}}</button> </td>
  </tr>
  <div>
    <div>
      <div
       class="fixed overflow-x-hidden overflow-y-auto inset-0 flex justify-center items-center z-50"
       v-if="toggleModal"
       >
        <div class="relative mx-auto w-auto max-w-2xl px-6">
          <div class="bg-white w-full rounded shadow-2xl flex flex-col">
            <div class="text-2xl font-mono"> {{toggleModal.name}}
          </div>
           
            <span cass="px-14 text-2xl font-mono"> {{toggleModal.description}} </span>
             <button
             class="rounded font-mono bg-purple-500 text-white px-6 mt-1 py-2 w=3/12 m-auto mb-3 " @click="toggleModal =false"
            > Voltar </button>
            </div>
         </div>
        </div>
      </div>
    <div v-if="toggleModal" class="absolute z-40 inset-0 opacity-25 bg-gray-500"></div>
 </div>
</div>
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
      search:"",
      selected: null,
      listDrinks: [],
      toggleModal: false
    }
  },
  mounted(){
    this.generateListDrinks()
  },
  computed: {
    filteredDrinks() {
    let filterDrinks: any = [];
      if(this.search){
        filterDrinks = this.listDrinks.filter((filterDrink: any) => {
      return (
        filterDrink.name.toLowerCase().indexOf(this.search.toLowerCase()) > - 1 )
    })

    return filterDrinks
      }
  
    filterDrinks = this.listDrinks.filter((filterDrink: any) => {
      if(this.selected === null){return filterDrink }
      return (
        filterDrink.category === this.selected
      )
    })
    return filterDrinks
   },
  },
  methods: {
    async generateListDrinks(): Promise<void> {
     await this.$axios
      .$get("http://localhost:3333/api/drinks")
      .then((response) => {
       this.listDrinks = response.data;
      })
    },
    clearFilter() {
      this.search = ""
      this.selected = null
    }
  },
})
</script>
