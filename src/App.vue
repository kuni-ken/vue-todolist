<template>
  <v-app>
    <v-main>
      <template>
        <ToDoDialog
          v-bind:show="showDialog"
          v-bind:todo="todo"
          v-on:doUpdate="doUpdate"
          v-on:cancel="dialogClose"
        />
        <v-card
          class="mx-auto"
          tile
        >
          <v-toolbar
            color="cyan"
            dark
          >
            <v-toolbar-title>ToDo一覧</v-toolbar-title>

            <v-spacer></v-spacer>

            <v-btn
              fab
              dark
              color="indigo"
              @click="onNewDialog"
            >
              <v-icon dark>
                mdi-plus
              </v-icon>
            </v-btn>
          </v-toolbar>
          <v-list outlined>
            <template>
              <v-list-item v-for="todo in todos" :key="todo.title">
                <template>
                  <v-list-item-content>
                    <v-list-item-title class="text-h5 mb-1">
                      {{ todo.title }}
                    </v-list-item-title>
                    <v-list-item-subtitle class="text-h5 mb-1">
                      {{ todo.detail }}
                    </v-list-item-subtitle>
                  </v-list-item-content>
                  <v-list-item-action>
                    <v-btn
                      outlined
                      rounded
                      text
                      @click="onShowDialog(todo.id)"
                    >
                      <v-icon>mdi-pencil-outline</v-icon>確認・変更
                    </v-btn>
                    <v-btn
                      outlined
                      rounded
                      text
                      @click="removeItem(todo.id)"
                    >
                      <v-icon>mdi-pencil-outline</v-icon>削除
                    </v-btn>
                  </v-list-item-action>
                </template>
              </v-list-item>

            </template>
          </v-list>
        </v-card>
        
      </template>
    </v-main>
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
      if (!todo.id){
        const time = new Date().getTime();
        this.todos.push({...todo, id: time});
      } else {
        const target = this.todos.find(el=>el.id===todo.id);
        Object.keys(target).map((v) => {
          target[v] = todo[v];
        })
      }
      this.dialogClose();
    },
    dialogClose(){
      this.showDialog = false;
    },
    onShowDialog(id){
      this.todo = this.todos.find(el=>el.id===id);
      this.showDialog = true;
    },
    onNewDialog(){
      this.todo = {};
      this.showDialog = true;
    },
    removeItem(id){
      this.todos = this.todos.filter(el=>el.id!==id);
    }
  },

  data(){
   const todos = [{
     id: 1,
     title: "鎌倉観光",
     detail: "鶴岡八幡宮\n→蕎麦屋\n→ジェラート屋\n→お土産屋"
   }]
   return {
     todos,
     todo: {},
     showDialog: false
   }
  },
};
</script>
