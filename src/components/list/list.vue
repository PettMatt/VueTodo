<template>
    <ul>
        <!-- :key on tapa merkitä elementti, jolla se voidaan eritellä muista elementeistä -->
        <!-- :key on lyhenne v-bind:key:stä -->
        <li v-for="(item, index) in todos" :key="index">
            <!-- Class bindaus. Kun todo.done arvo on true anna elementille done class -->
            <!-- Click Event. Kun elementtiä painetaan toteuta toggleDone funktio -->
            <h3 :class="{ done: item.done }" @click="doneToggle(item)">
                <span>{{ index + 1 }})</span>
                {{ item.content }}
                <button @click="removeTodo(index)">Remove</button>
            </h3>
        </li>
    </ul>
    <div v-if="!todos.length">
        <p>List is empty</p>
    </div>
</template>

<script>

export default {
    name: 'Input',
    props: {
        array: Object || Array,
        listName: String
    },
    setup() {
        function doneToggle(todo) {
            todo.done = !todo.done;
        }

        function removeTodo(index) {
            // Etsi todo indexin avulla ja poista se
            todos.value.splice(index, 1);
        }

        return {
            doneToggle,
            removeTodo,
        }
    }
}

// TODO:
// Luo yhteinen lista, johon kummallakin komponentilla on pääsy
// TAI
// Välitä luotu lista componenttiin, jossa ei ole pääsyä siihen
// TAI
// Tee äiti-komponenttiin lista, joka annetaan kummallekin

</script>

<style>

</style>