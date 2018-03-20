<template>
<div class="HelloWorld">
  <section class="section">
    <h1 class="title"> Menu <button @click="showAll">All</button> <button @click="showActive">Active</button> <button @click="showCompleted">Completed</button> <button @click="clearCompleted">Clear Completed</button> </h1> 
    <input v-model="newTask"> <button @click="addTask">Add a new task</button>
    <div v-for="(item, index) in tasks" v-if="item.show">
      {{item.name}} <button @click="item.status=!item.status"> {{item.status ? "(✔)" : "( )"}} </button> <button @click="edit(index)">Edit</button> <div v-if="tasks[index].edition"> <input v-model="tasks[index].name"> <button @click="tasks[index].edition=!tasks[index].edition">OK</button> </div> <button @click="deleteTask(index)">Delete</button>
    </div>
  </section>
</div>
</template>

<script>
import "bulma/css/bulma.css";
export default {
  name: "HelloWorld",
  data() {
    return {
      newTask: "",
      tasks:[
      ]
    };
  },
  methods:{
    addTask(){
      this.tasks.unshift({
        name: this.newTask,
        status: false,
        show: true,
        edition: false,
      });
    },
    deleteTask(i){
      this.tasks.splice(i, 1);
    },
    showAll(){
      for (var i=0;i<this.tasks.length;i++){
        this.tasks[i].show=true;
      }
    },
    showActive(){
      for (var i=0;i<this.tasks.length;i++){
        if (this.tasks[i].status==false){
          this.tasks[i].show=true;
        }else{
          this.tasks[i].show=false;
        }
      }
    },
    showCompleted(){
      for (var i=0;i<this.tasks.length;i++){
        if (this.tasks[i].status==true){
          this.tasks[i].show=true;
        }else{
          this.tasks[i].show=false;
        }
      }
    },
    edit(i){
      this.tasks[i].edition=true;
    },
    clearCompleted(){
      for (var i=0;i<this.tasks.length;i++){
        if (this.tasks[i].status){
          this.tasks[i].name=null;
          this.tasks[i].show=null;
          this.tasks[i].status=null;
        }
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/*h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}*/
</style>
