<template>
  <div class="container">
      <h2 class="text-center mt-5">My Vue Todo App</h2>

      <div class="d-flex">
        <input v-model="task" type="text" placeholder="Enter Task" class="form-control">
        <button @click="submitTask" type="submit" class="btn btn-warning rounded-0">Submit</button>
      </div>

      <table class="table table-borderless">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Task</th>
            <th scope="col">Status</th>
            <th scope="col">#</th>
            <th scope="col">#</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task,index) in tasks" :key="index">
            <th scope="row">1</th>
            <td>{{task.name}}</td>
            <td>
              <span class="pointer" @click="changeStatus(index)">
                 {{task.status}}
              </span>
            </td>
            <td>
              <div class="text-center pointer" @click="editTask(index)">
                <span class="fa fa-pen"></span>
              </div>
            </td>
            <td>
              <div class="text-center pointer" @click="deleteTask(index)">
                <span class="fa fa-trash"></span>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return{
      task: "",
      editedTask : null,
      availableStatus: ["to-do","In Progress", "Finished"],
      tasks: [
        {
          name: "memasak",
          status: "to-do" 

        }
      ]
    }
  },

  methods:{
    submitTask(){
        if(this.task.length === 0) return;
        if(this.editedTask === null){
          this.tasks.push({
            name: this.task,
            status: "to-do"
          })   
        }else{
          this.tasks[this.editedTask].name = this.task;
          this.editedTask = null
        }

        this.task = ''
    },
    deleteTask(index){
      this.tasks.splice(index,1)
    },
    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index){
      let newIndex = this.availableStatus.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.availableStatus[newIndex];
    }
  }
}
</script>
<style scoped>
.pointer {
  cursor: pointer;
}
</style>

