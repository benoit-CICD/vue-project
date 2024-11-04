<template>
    <div class="list-container">
      <template v-for="liste in filterTodo" :key="liste.id">
        <li class="list-item">
          <span :class="liste.done ? 'active' : ''">{{ liste.title }}</span>
          <input type="checkbox" v-model="liste.done" />
          <!-- <label>{{ liste.done ? 'Fait' : 'À faire' }}</label> -->
        </li>
      </template>
    </div>
  
    <div class="ajout-liste">
      <input type="text" v-model="newTask" placeholder="Ajouter Tâche" class="input-task" />
      <button @click="ajout()" class="btn-add">+</button>
    </div>
  
    <div class="cacher-liste">
      <button @click="toggleFilter" class="btn-filter"> {{ labelFilter }}</button>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue'
  
  const listes = ref([
    { id: 1, title: 'Installation', done: false },
    { id: 2, title: 'Mise en test', done: false },
    { id: 3, title: 'Déploiement', done: false }
  ])
  
  const filterTodo = computed(() => {
    return cacher.value ? listes.value.filter((liste) => !liste.done) : listes.value
  })
  
  const newTask = ref('')
  const cacher = ref(true)
  
  const labelFilter = computed(() => {
    return cacher.value ? "Afficher Toutes" : "Cacher complétées"
  })
  
  const ajout = () => {
    if (newTask.value.trim()) {
      listes.value.push({
        id: listes.value.length + 1,
        title: newTask.value,
        done: false
      })
      newTask.value = ''
    }
  }
  
  const toggleFilter = () => {
    cacher.value = !cacher.value
  }
  </script>
  
  <style scoped>
  .list-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 10px;
    background-color: #f9f9f9;
    border: 1px solid #ddd;
    border-radius: 8px;
  }
  
  .list-item {
    margin: 8px 0;
    padding: 10px;
    background-color: #fff;
    border-radius: 4px;
    border: 1px solid #ddd;
    list-style-type: none;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  
  .active {
    text-decoration: line-through;
  }
  
  /* Styles pour la section d'ajout de tâche */
  .ajout-liste {
    display: flex;
    justify-content: center; /* Centre l'ensemble du conteneur */
    margin: 10px 0;
  }
  
  .input-task {
    width: 200px; /* Largeur fixe pour l'input */
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
    margin-right: 10px; /* Espace entre l'input et le bouton */
  }
  
  .btn-add {
    padding: 10px;
    background-color: #28a745; /* Couleur verte */
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .btn-add:hover {
    background-color: #218838; /* Couleur verte plus sombre au survol */
  }
  
  /* Styles pour le bouton de filtre */
  .cacher-liste {
    display: flex;
    justify-content: center;
    margin-top: 10px;
  }
  
  .btn-filter {
    padding: 10px 20px;
    background-color: #007bff; /* Couleur bleue */
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .btn-filter:hover {
    background-color: #0056b3; /* Couleur bleue plus sombre au survol */
  }
  </style>
  