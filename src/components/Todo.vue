<template>
  <div>
      <q-card>
          <q-card-main>
                <h5>Todo List</h5>
                <q-input type="text" v-model="holder" stack-label="Enter Todo" />
                <q-btn id="selectAll" @click="add_todo">Add Todo</q-btn>

                <hr/>
                <q-list v-if="not_done_todos">
                    <q-item v-for="(todo,index) in not_done_todos" v-bind:key="index">
                        <div>
                            <label>
                                <input type="checkbox" @click="done_todo(todo.todo)"  :value="todo.todo" :checked="todo.status"/> {{todo.todo}}
                            </label>
                        </div>
                    </q-item>
                </q-list><br/>
                <div class="todo-footer" v-if="not_done_todos">
                    <strong><span class="count-todos">{{not_done_todos.length}}</span></strong> Item(s) Left
                </div>
          </q-card-main>
      </q-card>
  </div>
</template>

<script>
  import {
    QBtn,
    QIcon,
    QList,
    QListHeader,
    QItem,
    QItemSide,
    QItemMain,
    QInput,
    QCard,
    QCardMain,
    Alert
  } from 'quasar'
  
  export default {
    name: 'todo',
    components: {
      QBtn,
      QIcon,
      QList,
      QListHeader,
      QItem,
      QItemSide,
      QItemMain,
      QInput,
      QCard,
      QCardMain
    },
    data () {
      return {
        holder: ''
      }
    },
    methods: {
      add_todo: function () {
        if (this.holder.length < 1) {
          Alert.create({html: 'Please enter a todo item!'})
        }
        else {
          this.$store.dispatch('ADD_TODO', this.holder)
          this.holder = ''
        }
      },
      done_todo: function (todo) {
        this.$store.dispatch('COMPLETE_TODO', todo)
      }
    },
    computed: {
      not_done_todos: function () {
        return this.$store.getters.not_done
      }
    }
  }
</script>

<style></style>