<template>
  <v-app>
    <v-container text-center wrap md12>
      <v-app-bar color="info" dark app>
        <v-toolbar-title>ToDo List</v-toolbar-title>
      </v-app-bar>
      <v-card class="mx-auto" outlined max-width="1200" @submit.prevent>
        <v-card-title>
          <v-text-field 
          label="入力欄" 
          placeholder="ToDoの入力" 
          outlined
          single-line
          hide-details
          v-model="task" 
          @keyup.enter="add()" 
          @click:append="add()" 
          append-icon="mdi-square-edit-outline">
          </v-text-field>
        </v-card-title>
        <v-btn icon ripple>
            <v-menu>
              <template v-slot:activator="{ on }">
                <v-icon color="grey lighten-1" v-on="on">mdi-calendar-month-outline
                </v-icon>
              </template>
              <v-date-picker
              v-model="picker"
              reactive locale="jp-ja"
              :day-format="date => new Date(date).getDate()"
              no-title
              scrollable>
                <v-btn flat color="primary" @click="picker = ' ' ">Delete</v-btn>
                <v-btn flat color="primary" @click="$refs.menu.save(picker)">OK</v-btn>
              </v-date-picker>
            </v-menu>
        </v-btn>
        <span class="text-sm-left">{{picker}}</span>
        <v-btn icon ripple>
            <v-menu>
              <template v-slot:activator="{ on }">
                <v-icon color="grey lighten-1" v-on="on">mdi-folder
                </v-icon>
              </template>
              <v-text-field solo hide-details @click.stop=""/>
            </v-menu>
        </v-btn>
        <span class="text-sm-left">{{memo}}</span>
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
        width: "70%"
      },
      {
        text: "Date",
        sortable: true,
        value: "picker"
      },
      {
        text: "Memo",
        sortable: true,
        value: "memo"
      },
      {
        text: "Action",
        sortable: false,
        value: "control"
      },
    ],
    items: [],
    task: "",
    picker: ""
  }),
  methods: {
    add: function(){
      if(!this.task){
        return;
      }
      this.items.push({
          "task": this.task,
          "picker": this.picker
      });
        this.task = "";
        this.picker =""
    },
    deleteTodo: function(item) {
      const result = confirm("削除してもよろしいですか？")
      if(result) {
      this.items.splice(this.items.indexOf(item), 1);
      }
    },
    editTodo: function() {

    }
  },
}
</script>