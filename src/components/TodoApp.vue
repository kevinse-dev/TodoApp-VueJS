<template>
  <div class="hello">
    Your Todo List App
    <div class="container">
      <h2 class="text-center mt-5"></h2>
      <!-- Input -->
      <div class="d-flex">
        <input v-model="task" type="text" placeholder="Enter your Task" class="form-control" />
        <button @click="submitTask" class="btn btn-primary px-5">Submit</button>
      </div>

      <!-- Table List -->
      <table class="table table-bordered mt-5">
        <thead>
          <tr>
            <th scope="col">Task</th>
            <th scope="col" class="text-center">Status</th>
            <th scope="col" class="text-center">#</th>
            <th scope="col" class="text-center">#</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="( task, index ) in tasks" :key="index">
            <td>
              <span :class="{'finished': task.status === 'Finished'}" >{{ task.name }}</span>
              </td>
            <td>
              <h5 class="pointer" @click="changeStatus(index)"
                    :class="{'text-danger': task.status === 'To-do', 'text-warning': task.status === 'In-Progress', 'text-success': task.status === 'Finished'}"
              
              >{{ task.status }}</h5>
              </td>
            <td>
              <div class="text-center pointer" @click="updateTask(index)">
                <span class="fa fa-pen"></span>
              </div>
            </td>
            <td>
              <div class="text-center pointer"  @click="deleteTask(index)">
                <span class="fa fa-trash"></span>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoAPp",
  data() {
    return {
      task:'',
      editedTask:null,
      availabelStatus:['To-do', 'In-Progress', 'Finished'],
      tasks: [
        {
          name: "Steal bananas from store.",
          status: "To-do",
        },
        {
          name: "Eat 1kg chocolate in 1 hour",
          status: 'In-Progress'
        },
      ],
    };
  },
  methods:{
    submitTask(){
      if(this.task === '') return;
      if(this.editedTask === null){
        this.tasks.push({
          name:this.task,
        status:'To-do'
      })
        }else{
          this.tasks[this.editedTask].name = this.task
          this.editedTask = null
        }
          this.task = ''
    },
    deleteTask(index){
      this.tasks.splice(index, 1)
    },
    updateTask(index){
      this.task = this.tasks[index].name
      this.editedTask = index
    },
    changeStatus(index){
      let newIndex = this.availabelStatus.indexOf(this.tasks[index].status)
      if(++newIndex > 2) newIndex = 0
      this.tasks[index].status = this.availabelStatus[newIndex]
}
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.pointer{
  cursor: pointer;
}
.finished{
  text-decoration: line-through;
}
</style>
