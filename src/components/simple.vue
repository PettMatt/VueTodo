<template>
    <h2>{{ listName }}-list</h2>
    <form @submit.prevent="addNewTodo">
        <label for="newTodo">New Todo</label>
        <!-- Bindataan muuttuja html-elementtiin -->
        <input v-model="newTodo" name="newTodo" autocomplete="off">
        <button type="submit">Add</button>
    </form>
    <button @click="markAllDone()">Mark all done</button>
    <button @click="clearTodos()">Clear todos</button>
    <ul v-if="todos.length">
        <!-- :key on tapa merkitä elementti, jolla se voidaan eritellä muista elementeistä -->
        <!-- :key on lyhenne v-bind:key:stä -->
        <li v-for="(item, index) in todos" :key="index">
            <!-- Class bindaus. Kun todo.done arvo on true anna elementille done class -->
            <!-- Click Event. Kun elementtiä painetaan toteuta toggleDone funktio -->
            <h3 :class="{ done: item.done }" @click="doneToggle(item)">
                <span>{{ index + 1 }})</span>
                {{ item.content }}
            </h3>
            <button @click="removeTodo(index)">X</button>
        </li>
    </ul>
    <div v-if="!todos.length">
        <p>List is empty</p>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    name: 'Simple',
    // Propsien avulla voidaan tuoda arvoja äitikomponentista
    props: {
        listName: String,
    },
    setup() {
        // Ref on tapa tuottaa reaktiivinen arvo, joka muuttaa arvoaan kun muuttujaan tehdään muutoksia
        const newTodo = ref('');
        const done = ref('');
        const todos = ref([]);

        function addNewTodo() {
            todos.value.push({
                done: false,
                content: newTodo.value
            });

            // Input on data bindingin alaisuudessa, joten jos newTodo:n arvoa muutetaan muuttuu myös data bindatun elementin arvo
            newTodo.value = '';
        }

        function doneToggle(todo) {
            todo.done = !todo.done;
        }

        function removeTodo(index) {
            // Etsi todo indexin avulla ja poista se
            todos.value.splice(index, 1);
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
            done,
            todos,
            newTodo,
            addNewTodo,
            clearTodos,
            doneToggle,
            removeTodo,
            markAllDone
        }
    }
}

</script>

<style>
body {
    margin-left: 0px;
    margin-right: 0px;
}

.done {
    opacity: 0.6;
    text-decoration: line-through;
}

li {
    display: block ruby;
    width: 100%;
}

ul {
    height: 70vh;
    padding-left: 0px;
    overflow-y: scroll;
}

h3 {
    color: #000;
}

li h3 {
    padding: 0 5px;
    width: 50%;
    text-align: left;
    cursor: pointer;
}

button {
    background-color: rgba(0,0,0,0);
    cursor: pointer;
}

button, input {
    border: 3px solid #000;
    padding: 5px;
    margin: 5px 5px;
    border-radius: 5px;
}
</style>