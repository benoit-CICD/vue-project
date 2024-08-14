<template>
    <h1>Bonjour</h1>
    <p>Compteur : {{ count }}</p>
<!--     <p :class="{active: count > 5}"  v-bind:id="`p-${count}`">Compteur : {{ count }} </p> -->
<!--     <p :style="{color: count > 5 ? 'red' : 'green'}" v-bind:id="`p-${count}`">Compteur : {{ count }} </p> -->
<!--     <div v-if="count >= 5">Bravo vous avez cliqué plus de 5 fois</div>
    <div v-else> Vous avez cliqué moins de 5 fois</div> -->
    <button v-on:click="increment">Incrémenter</button>
    <button @click="decrement">Décrémenter</button>
    <button @click="sortMovies">Réorganiser</button>

    <form action="" @submit.prevent="addMovie">
        <input type="text" placeholder="Nouveau film..." v-model="movieName"> 
        <button>
            Ajouter
        </button>
    </form>
    <ul>
        <li 
            v-for="movie in movies"
            :key="movie"
        >
            {{ movie }} <button @click="deleteMovie(movie)">Supprimer</button>
        </li>
    </ul>
<!--     <div v-text="firstname"></div> -->
    <br><br>
    <ul>
        <li>{{ person.firstname }}</li>
        <li>{{ person.lastname }}</li>
        <li>{{ person.age }}</li>
        
    </ul>
    <button @click.prevent="randomAge">Changer age</button>
    
</template>

<script setup>

import {ref} from 'vue'
    const count = ref(0)

    const movies = ref([
        'Rush',
        'The Fall Guy',
        'Les Affranchis'
    ])

    const sortMovies = () => {
        movies.value.sort((a,b) => a > b ? 1 : -1)
    }

    const deleteMovie = (movie) => {
        movies.value = movies.value.filter(m => m !== movie)
    }

    const movieName = ref('')

    const addMovie = () => {
        movies.value.push(movieName.value)
        movieName.value = ''
    }

    const firstname = '<span>DEMO</span>'
    const increment = (event) => {
        console.log(count, count.value)
        count.value++
    }

    const person = ref({
        firstname: 'John',
        lastname: 'Doe',
        age: 20
    })

    const randomAge = () => {
            person.value.age =  Math.round(Math.random() * 100)
        
    }


    const decrement  = () => {
        count.value--
    }

/*     setInterval(()=>  {
        count.value++
    }, 1000);
 */
</script>

<style>
h1 {
    color: violet;
}

.active {
    color: red;
}
</style>