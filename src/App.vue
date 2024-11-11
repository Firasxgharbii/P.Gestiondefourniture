<template>
  <div id="app" class="min-h-screen bg-gray-100 flex items-center justify-center">
    <div class="w-full max-w-lg p-6 bg-white rounded-lg shadow-lg">
      <h1 class="text-3xl font-bold text-center mb-6 text-gray-800">Gestion de Fournitures</h1>
      <FournitureForm @ajouter-fourniture="ajouterFourniture" />
      <FournitureList
        :fournitures="fournitures"
        @supprimer-fourniture="supprimerFourniture"
        @edit-fourniture="editFourniture"
      />
    </div>
  </div>
</template>

<script>
import FournitureForm from './components/FournitureForm.vue';
import FournitureList from './components/FournitureList.vue';

export default {
  components: {
    FournitureForm,
    FournitureList
  },
  data() {
    return {
      fournitures: JSON.parse(localStorage.getItem('fournitures') || '[]')
    };
  },
  methods: {
    ajouterFourniture(fourniture) {
      this.fournitures.push(fourniture);
      this.saveFournitures();
    },
    supprimerFourniture(index) {
      this.fournitures.splice(index, 1);
      this.saveFournitures();
    },
    editFourniture(updatedFourniture, index) {
      this.fournitures.splice(index, 1, updatedFourniture);
      this.saveFournitures();
    },
    saveFournitures() {
      localStorage.setItem('fournitures', JSON.stringify(this.fournitures));
    }
  }
};
</script>

<style>
/* Style global pour un design harmonieux */
body {
  font-family: 'Arial', sans-serif;
  background-color: #f9fafb;
}
</style>
