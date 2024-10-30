<template>
    <div class="list-container">
      <template v-for="liste in filterTodo" :key="liste.id">
        <li class="list-item">
        <span :class="liste.done ? 'active' : ''">{{ liste.title }}</span>
          <input type="checkbox" v-model="liste.done" />
         <!--  <label>{{ liste.done ? 'Fait' : 'À faire' }}</label> -->
        </li>
      </template>
    </div>
  
    <div class="ajout-liste">
      <input type="text" v-model="newTask" placeholder="Ajouter Tâche" />
      <button @click="ajout()">+</button>
    </div>

    <div class="cacher-liste">
      <button @click="cacher = !cacher"> {{ labelFilter }}</button>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue'
  
  const listes = ref([
    { id: 1, title: 'Installation', done: false },
    { id: 2, title: 'Mise en test', done: false },
    { id: 3, title: 'Déploiement', done: false }
  ])

  const filterTodo  = computed(()=> {
    return cacher.value ? listes.value : listes.value.filter((liste) => !liste.done)
  })
  
  const newTask = ref('');

  const cacher = ref(true);
  const labelFilter = computed(() => {
    return cacher.value ? "Caché complété" : "Afficher Toutes";
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


  </style>
  