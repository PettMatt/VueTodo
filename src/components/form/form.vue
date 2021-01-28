<template>
    <form @submit.prevent="addNewTodo(listName)">
        <h2>{{ listName }}</h2>
        <!-- Bindataan muuttuja html-elementtiin -->
        <input v-model="newTodo" name="newTodo" autocomplete="off">
        <button type="submit">Add</button>
    </form>
    <button @click="markAllDone()">Mark all done</button>
    <button @click="clearTodos()">Clear todos</button>
</template>

<script>
import { ref } from 'vue';

export default {
    name: 'Form',
    props: {
        array: Object || Array,
        listName: String
    },
    setup() {
        // Ref on tapa tuottaa reaktiivinen arvo, joka muuttaa arvoaan kun muuttujaan tehdään muutoksia
        const newTodo = ref('');
        //const todos = array;

        // TODO: Lisää input list-komponenttiin, jotta voidaan eritellä erit listat
        function addNewTodo(listName) {
            todos.value.push({
                listName: listName,
                done: false,
                content: newTodo.value
            });

            // Input on data bindingin alaisuudessa, joten jos newTodo:n arvoa muutetaan muuttuu myös data bindatun elementin arvo
            newTodo.value='';
        }

        function markAllDone() {
            todos.value.forEach((todo) => todo.done = true);
        }

        function clearTodos() {
            todos.value = [];
        }

        // Mitä ikinä tässä palautetaan voidaan käyttää myös kyseisen componentin templatessa
        // Esim. Jollei todos listaa välitetä returnin kautta templaten data binding ei tiedä mistä data bindattu arvo tulee
        return {
            todos,
            newTodo,
            addNewTodo,
            clearTodos,
            markAllDone
        }
    }
}

</script>

<style>
.done {
    color: #567;
    text-decoration: line-through;
}
</style>