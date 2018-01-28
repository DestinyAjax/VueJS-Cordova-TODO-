<template>
    <div>
        <q-card>
            <q-card-main>
                <h5>Already Done</h5>
                <q-list v-if="done_todos">
                    <q-item v-for="(todo,index) in done_todos" v-bind:key="index">
                         {{todo.todo}}
                    </q-item>
                </q-list>
            </q-card-main>
        </q-card>
    </div>
</template>

<script>
 import {
   QList,
   QItem,
   QCard,
   QCardMain
 } from 'quasar'

 export default {
   name: 'done',
   components: {
     QList,
     QItem,
     QCard,
     QCardMain
   },
   methods: {
   },
   computed: {
     done_todos: function () {
       return this.$store.getters.done
     }
   }
 }
</script>

<style>
</style>