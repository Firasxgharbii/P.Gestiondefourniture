<template>
    <div class="max-w-lg mx-auto mt-4">
      <input
        type="text"
        v-model="searchTerm"
        placeholder="Rechercher une fourniture..."
        class="shadow appearance-none border rounded w-full py-2 px-3 mb-4 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
      />
      <ul class="space-y-2">
        <li
          v-for="(fourniture, index) in filteredFournitures"
          :key="index"
          class="flex items-center justify-between bg-white p-4 rounded-lg shadow-md"
        >
          <div>
            <span class="font-semibold text-gray-700">{{ fourniture.nom }}</span>
            <span class="text-gray-600"> - Quantité : {{ fourniture.quantite }}</span>
          </div>
          <div class="flex space-x-2">
            <button
              @click="editFourniture(index)"
              class="bg-yellow-500 hover:bg-yellow-700 text-white font-bold py-1 px-2 rounded"
            >
              Modifier
            </button>
            <button
              @click="supprimerFourniture(index)"
              class="bg-red-500 hover:bg-red-700 text-white font-bold py-1 px-2 rounded"
            >
              Supprimer
            </button>
          </div>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      fournitures: {
        type: Array,
        required: true
      }
    },
    data() {
      return {
        searchTerm: ''
      };
    },
    computed: {
      filteredFournitures() {
        return this.fournitures.filter(fourniture =>
          fourniture.nom.toLowerCase().includes(this.searchTerm.toLowerCase())
        );
      }
    },
    methods: {
      supprimerFourniture(index) {
        this.$emit('supprimer-fourniture', index);
      },
      editFourniture(index) {
        const fourniture = this.fournitures[index];
        const newNom = prompt("Modifier le nom :", fourniture.nom);
        const newQuantite = prompt("Modifier la quantité :", fourniture.quantite);
  
        if (newNom && newQuantite > 0) {
          this.$emit('edit-fourniture', { nom: newNom, quantite: parseInt(newQuantite) }, index);
        }
      }
    }
  };
  </script>
  