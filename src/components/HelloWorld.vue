<template>
  <v-app>
    <v-container text-center wrap md12>
      <v-app-bar color="info" dark app>
        <v-toolbar-title>ToDo List</v-toolbar-title>
      </v-app-bar>
      <v-card class="mx-auto" outlined max-width="1200" @submit.prevent>
        <v-card-title>
          <v-text-field label="入力欄" placeholder="ToDoの入力" outlined v-model="task" @keyup.enter="add()" @click:append="add()" append-icon="mdi-square-edit-outline"></v-text-field>
        </v-card-title>
        <v-data-table :headers="headers" :items="items" :things-per-page="5" class="elevation-1">
          <template v-slot:item.control="{ item }">
            <v-btn class="mx-2" fab dark x-small color="info" @click="editTodo(item)">
              <v-icon>mdi-square-edit-outline</v-icon>
            </v-btn>  
            <v-btn class="mx-2" fab dark x-small color="info" @click="deleteTodo(item)">
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </template>
        </v-data-table>
       <v-date-picker v-model="picker" reactive locale="jp-ja" :day-format="date => new Date(date).getDate()"></v-date-picker>
       <v-footer color="info" dark app>ToDo List</v-footer>
      </v-card> 
    </v-container>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    headers: [
      {
        text: "ToDo",
        sortable: true,
        value: "task",
        datetime : "",
        width: "70%"
      },
      {
        sortable: false,
        value: "control"
      },
    ],
    items: [],
    task: "",
  }),
  methods: {
    add: function(){
      if(!this.task){
        return;
      }
      this.items.push({
          "task": this.task,
          datetime : "",
      });
        this.task = "";
    },
    deleteTodo: function(item) {
      const result = confirm("削除してもよろしいですか？")
      if(result) {
      this.items.splice(this.items.indexOf(item), 1);
      }
    },
    editTodo: function() {

    }
  }
}
</script>