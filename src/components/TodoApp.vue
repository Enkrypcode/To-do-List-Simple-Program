<template>

  <div class="container" style="max-width: 600px">
    <h1 class="text-center mt-5">To-Do List</h1>
  </div>

  <!-- input -->
  <div class="d-flex mt-5" style="margin-left: 300px; margin-right: 300px">
    <input v-model="task" type="text" class="form-control w-100" placeholder="Enter task">
    <button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
  </div>

  <!-- task table -->
  <div style="margin-left: 300px; margin-right: 300px">
    <table class="table table-bordered mt-5 ">
      <thead>
        <tr>
          <th scope="col" style="width: 60%">Task</th>
          <th scope="col" style="width: 150px">Status</th>
          <th scope="col" class="text-center" style="width: 100px">Progress</th>
          <th scope="col" class="text-center" style="width: 100px">Delete</th>
        </tr>
      </thead>
      <tbody>

        <tr v-for="(task,index) in tasks" :key="index">
          <!-- FOR LOOP / UNIQUE ITERATION.. Reorder/reuse existing element-->
          <th>{{task.name}}</th>
          <td style="width: 120px;">
            <span @click="changeStatus(index)" class="pointer" style="cursor: pointer;">
              {{task.status}}</span>
          </td>
          <td>
            <div class="text-center" @click="editTask(index)">
              <span class="fa fa-pen pointer" style="">
              </span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
              <span class="fa fa-trash pointer"  style="cursor: pointer;"></span>
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
    data() {
      return {
        task: '',
        editedTask: null,
        availableStatuses: ['To-do', 'In-progress', 'Finished'],
        tasks: []
      }
    },
    methods: {
      submitTask() {
        if (this.task.length === 0) return;

        if (this.editedTask === null) {
          this.tasks.push({
            name: this.task,
            status: 'To-do'
          });
        } else {
          this.tasks[this.editedTask].name = this.task;
          this.editedTask = null
        }
        this.task = '';

      },
      deleteTask(index) {
        this.tasks.splice(index, 1);
      },

      editTask(index) {
        this.task = this.tasks[index].name;
        this.editedTask = index;
      },

      changeStatus(index){
        let newIndex = this.availableStatuses.indexOf(this.tasks[index].status)
        if(++newIndex > 2) newIndex = 0;
        this.tasks[index].status = this.availableStatuses[newIndex];
      }
    }
  };
</script>