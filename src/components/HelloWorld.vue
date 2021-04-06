<template>
  <v-app>
    <v-container text-center wrap md12>
      <v-app-bar color="info" dark app>
        <v-toolbar-title>ToDo List</v-toolbar-title>
      </v-app-bar>
      <v-card class="mx-auto" outlined max-width="1200">
        <v-card-title> 
          <v-text-field label="入力欄" placeholder="ToDoの入力" outlined></v-text-field>
            <v-btn color="primary" dark class="mb-2">追加</v-btn>
        </v-card-title> 
        <v-data-table :headers="headers" :things="things" :items-per-page="5" class="elevation-1">
          <template v-slot:thing.control="{ thing }">
            <v-btn class="mx-2" fab dark x-small color="error" @click="deleteTask(thing)">
              <v-icon dark>mdi-minus</v-icon>
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
        value: "title",
        width: "70%"
      },
      {
        text: "削除",
        sortable: false,
        value: "control"
      },
    ],
    things: [],
    title: "",
  })  
}
</script>