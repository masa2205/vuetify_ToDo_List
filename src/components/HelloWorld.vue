<template>
  <v-app>
    <v-app-bar color="#4DD0E1" dark app>
      <v-toolbar-title class="font-italic">ToDo List</v-toolbar-title>
    </v-app-bar>
    <v-img
     lazy-src="https://picsum.photos/id/11/10/6"
     max-height="auto"
     max-width="auto"
     src="https://picsum.photos/id/11/500/300">
      <v-container text-center wrap md12>
        <v-card class="mx-auto" outlined max-width="1600" @submit.prevent>
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
              <v-menu transition="fab-transition">
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
                  <v-btn flat color="primary" @click="picker = '' ">Delete</v-btn>
                  <v-btn flat color="primary" @click="$refs.menu.save(picker)">OK</v-btn>
                </v-date-picker>
              </v-menu>
          </v-btn>
          <span class="text-sm-left">{{picker}}</span>
          <v-btn icon ripple>
              <v-menu transition="scale-transition">
                <template v-slot:activator="{ on }">
                  <v-icon color="grey lighten-1" v-on="on">mdi-alarm
                  </v-icon>
                </template>
                <v-time-picker
                v-model="time"
                ampm-in-title
                format="24hr">
                  <v-btn flat color="primary" @click="time = '' ">Delete</v-btn>
                  <v-btn flat color="primary" @click="$refs.menu.save(time)">OK</v-btn>
                </v-time-picker>
              </v-menu>
          </v-btn>
          <span class="text-sm-left">{{time}}</span>
          <v-btn icon ripple>
              <v-menu transition="fab-transition">
                <template v-slot:activator="{ on }">
                  <v-icon color="grey lighten-1" v-on="on">mdi-folder
                  </v-icon>
                </template>
                <v-text-field
                single-line
                solo 
                append-icon="mdi-square-edit-outline" 
                label="入力欄" 
                placeholder="Memoの追加" 
                hide-details 
                v-model="memo" 
                @click.stop="">
                </v-text-field>
              </v-menu>
          </v-btn>
          <span class="text-sm-left" >{{memo}}</span>
          <v-data-table :headers="headers" :items="items" :things-per-page="5" class="elevation-1">
            <template v-slot:item.control="{ item }">
                <v-btn class="mx-2" fab dark x-small color="info" @click="editTodo(item)">
                  <v-menu transition="scale-transition">
                    <template v-slot:activator="{ on }">
                      <v-icon color="grey lighten-1" v-on="on">mdi-square-edit-outline
                      </v-icon>
                    </template>
                    <v-text-field
                    single-line
                    solo 
                    append-icon="mdi-square-edit-outline" 
                    hide-details 
                    label="入力欄"
                    placeholder="ToDoの編集"
                    @click.stop="">
                    </v-text-field>
                  </v-menu>
                </v-btn>  
                <v-btn class="mx-2" fab dark x-small color="info" @click="deleteTodo(item)">
                  <v-icon>mdi-delete</v-icon>
                </v-btn>
            </template>
          </v-data-table>
         <v-footer color="#4DD0E1" dark app class="font-italic">ToDo List</v-footer>
        </v-card> 
      </v-container>
    </v-img>
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
        sortable: false,
        value: "picker"
      },
      {
        text: "Time",
        sortable: false,
        value: "time"
      },
      {
        text: "Memo",
        sortable: false,
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
    picker: "",
    time: "",
    memo:""
  }),
  methods: {
    add: function(){
      if(!this.task){
        return;
      }
      this.items.push({
          "task": this.task,
          "picker": this.picker,
          "time": this.time,
          "memo": this.memo
      });
      this.task = "";
      this.picker = "";
      this.time = "";
      this.memo = ""
      this.saveList();
    },
    deleteTodo: function(item) {
      const result = confirm("削除してもよろしいですか？")
      if(result) {
      this.items.splice(this.items.indexOf(item), 1);
      }
      this.saveList();
    },
    editTodo: function() {
      this.items[0] = ""
    },
    saveList: function(){
      localStorage.setItem('items', JSON.stringify(this.items));
    },
    loadList: function(){
           this.items=JSON.parse(localStorage.getItem('items'));
           if(!this.items){
               this.items=[];
           }
    },
    mounted: function(){
           this.loadList();
    }
  }
}
</script>