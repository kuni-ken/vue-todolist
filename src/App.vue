<template>
  <v-app>
    <template>
      <ToDoDialog
        v-bind:show="showDialog"
        v-bind:todo="todo"
        v-on:doUpdate="doUpdate"
        v-on:cancel="dialogClose"
      />
      <v-card
        class="mx-auto"
        max-width="344"
        outlined
      >
        <v-list-item three-line>
          <v-list-item-content>
            <v-list-item-title class="text-h5 mb-1">
              {{ todo.title }} {{ todo.detail }}
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-card-actions>
          <v-btn
            outlined
            rounded
            text
            @click="showDialog = true"
          >
            確認・変更
          </v-btn>
        </v-card-actions>
      </v-card>
    </template>
  </v-app>
</template>

<script>
import ToDoDialog from './components/ToDoDialog';

export default {
  name: 'App',

  components: {
    ToDoDialog,
  },

  methods: {
    doUpdate(todo){
      Object.keys(this.todo).map((v) => {
        this.todo[v] = todo[v];
      })
      this.dialogClose();
    },
    dialogClose(){
      this.showDialog = false;
    }
  },

  data(){
   const todo = {
     title: "鎌倉観光",
     detail: "鶴岡八幡宮\n→蕎麦屋\n→ジェラート屋\n→お土産屋"
   } 
   return {
     todo,
     showDialog: false
   }
  },
};
</script>
