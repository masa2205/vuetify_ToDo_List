<template>
  <v-app>
    <v-container text-center wrap md12>
      <v-app-bar color="info" dark app>
        <v-toolbar-title>ToDo List</v-toolbar-title>
      </v-app-bar>
      <v-text-field label="入力欄" placeholder="ToDoの入力" outlined></v-text-field>
      <v-checkbox
        v-model="showMessage"
        :label="`showMessage is ${showMessage}`"
        color="success">
      </v-checkbox>
     <v-date-picker
      v-model="picker"
      reactive
      locale="jp-ja"
      :day-format="date => new Date(date).getDate()"
    ></v-date-picker>
      <v-btn color="primary" dark @click="add()">追加</v-btn>
      <v-footer color="info" dark app>Vuetify</v-footer>
    </v-container>
  </v-app>
</template>

<script>

</script>