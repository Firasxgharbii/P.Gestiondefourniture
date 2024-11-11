<template>
    <form @submit.prevent="handleSubmit" class="bg-gray-50 shadow-md rounded-lg px-8 pt-6 pb-8 mb-6">
      <h2 class="text-2xl font-semibold text-gray-700 text-center mb-4">Ajouter une Fourniture</h2>
      <div class="mb-4">
        <label class="block text-gray-700 text-sm font-semibold mb-2" for="nom">Nom de la fourniture :</label>
        <input
          type="text"
          v-model="nom"
          id="nom"
          placeholder="Ex : Stylo, Papier, etc."
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          :class="{ 'border-red-500': nomError }"
        />
        <p v-if="nomError" class="text-red-500 text-xs italic">{{ nomError }}</p>
      </div>
      <div class="mb-6">
        <label class="block text-gray-700 text-sm font-semibold mb-2" for="quantite">Quantité :</label>
        <input
          type="number"
          v-model="quantite"
          id="quantite"
          min="1"
          placeholder="Ex : 10, 25, etc."
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
          :class="{ 'border-red-500': quantiteError }"
        />
        <p v-if="quantiteError" class="text-red-500 text-xs italic">{{ quantiteError }}</p>
      </div>
      <div class="flex items-center justify-center">
        <button
          type="submit"
          class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        >
          Ajouter Fourniture
        </button>
      </div>
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        nom: '',
        quantite: 1,
        nomError: null,
        quantiteError: null
      };
    },
    methods: {
      handleSubmit() {
        // Validation avancée
        this.nomError = this.nom ? null : "Le nom est obligatoire.";
        this.quantiteError = this.quantite > 0 ? null : "La quantité doit être supérieure à 0.";
  
        if (!this.nomError && !this.quantiteError) {
          this.$emit('ajouter-fourniture', { nom: this.nom, quantite: this.quantite });
          this.nom = '';
          this.quantite = 1;
        }
      }
    }
  };
  </script>
  