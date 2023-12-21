<template>
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
            <src> {{toggleModal.image}} </src> 
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


<script>
export default {
  name: 'DrinksModal',
  data() {
    return {
      toggleModal: false 
    };
  },
  methods: {

  },
  }
</script>
