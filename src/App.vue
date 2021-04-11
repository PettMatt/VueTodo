<template>
    <!--<img alt="Vue logo" src="./assets/logo.png">-->
    <!--<Input array=todos/>
    <Form array=todos listName="watching"/>
    <Form array=todos listName="reading"/>
    <Form array=todos listName="working"/>-->
    <Simple listName="Todo"/>
</template>

<script>
//import Form from './components/form/form.vue';
//import Input from './components/input/input.vue';
import Simple from './components/simple.vue';

import { ref } from 'vue';

export default {
    name: 'App',
    components: {
        //Form,
        //Input,
        Simple
    },
    setup() {
        // Yhteinen array, joka välitetään jokaiselle lapsikomponentille
        const todos = ref([]);

        return {
            todos
        }
    },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000;
  margin-top: 60px;
}
</style>
