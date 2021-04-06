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
       <v-date-picker v-model="picker" reactive locale="jp-ja" :day-format="date => new Date(date).getDate()"></v-date-picker>
       <v-footer color="info" dark app>ToDo List</v-footer>
      </v-card> 
    </v-container>
  </v-app>
</template>

<script>

</script>