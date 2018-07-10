<template>
  <div class="wrapper">
    <form @submit.prevent="">
        <div class="form-group">
          <input v-model="value" type="text" class="form-control" id="exampleInput" @keyup.enter="addTask">
          <input type="button" class="btn btn-primary" value="Add" v-on:click="addTask">
        </div>
      </form>
      <table class="table table-dark">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Task</th>
            <th scope="col">Remove</th>
          </tr>
        </thead>
        <tbody>
          <table-item v-for="(task,index) in tasks" 
          :title="task.title"
          :key="index"
          :myIndex="index +1"
          :check="task.check"
          @remove="removeTask(index)"
          @change="onChange(index, $event)">
          </table-item>     
        </tbody>
      </table>
      <button class="btn btn-warning" @click="deleteAll">Delete All</button>
      <button class="btn btn-info" @click="deleteCheck">Delete checked</button>
  </div>
</template>

<script>
import tableItem from './components/input.vue';

export default {
   data(){
    return {
      value: '',
      tasks: []
    }
  },
  components: {
    'table-item': tableItem
  },
  methods: {
    addTask(){
      if(this.value != ''){
        this.tasks.push({
          title: this.value,
          check: false
        });
      }
      this.value = '';
    },
    removeTask(index){
      this.tasks.splice(index, 1);
    },
    deleteAll(){
      this.tasks = [];
    },
    deleteCheck(){
      for(let i = 0; i < this.tasks.length; i++){
        console.log(i);
        if(this.tasks[i].check){
          console.log(i);
          this.tasks.splice(i, 1);
          i--;
          //console.log(this.tasks[i])
        }
      }
      /*this.tasks.forEach((element, i)=>{
          if(element.check){
            this.tasks.splice(i, 1);
          }
      });*/
    },
    onChange(index ,$event){
     // console.log(this.tasks[index]);
      this.tasks[index].check = $event;
    }
  }
  }
</script>

<style>
  form {
    margin-top: 50px;
  }
  .form-group {
    display: flex;
  }
</style>
