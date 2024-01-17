<script setup>
import { ref } from 'vue';

const tasks = ref([]);
const formTask = ref("");
const formTaskTime = ref("");

function addTask() {
  const newTask = {
    id: tasks.value.length + 1,
    name: formTask.value,
    Time: formTaskTime.value,
  };
  tasks.value.push(newTask);
  resetForm();
  hideAddTaskModal();
}

function removeTask(id) {
  tasks.value = tasks.value.filter(task => task.id !== id);
}


function hideAddTaskModal() {
  $('#myModal').modal('hide');
}

function resetForm() {
  formTask.value = "";
  formTaskTime.value = "";
}
</script>

<template>
  <div class="container mt-5">
    <h1 class="mb-4">Tasks List</h1>

    <ul class="list-group">
      <li v-for="task in tasks" :key="task.id" class="list-group-item d-flex justify-content-between align-items-center mt-3 mb-3">
        {{ task.name }} - {{ task.Time }} minutes
        <button @click="removeTask(task.id)" class="btn btn-danger ml-5">Remove</button>
      </li>
    </ul>

    <button type="button" class="btn btn-info btn-lg" data-toggle="modal" data-target="#myModal">Create a New Task</button>

 
    <!-- End Bootstrap Modal -->
  </div>


<!-- Modal -->
<div id="myModal" class="modal fade" role="dialog">
  <div class="modal-dialog">

    <!-- Modal content-->
    <div class="modal-content">
      <div class="modal-header">
        <h4 class="modal-title">Add New Task</h4>
        <button type="button" class="close" data-dismiss="modal">&times;</button>
        
      </div>
      <div class="modal-body text-left">
        <form @submit.prevent="addTask">
              <div class="mb-3">
                <label for="taskName" class="form-label">Task Name:</label>
                <input v-model="formTask" type="text" id="taskName" class="form-control" required>
              </div>

              <div class="mb-3">
                <label for="taskTime" class="form-label">Time (minutes):</label>
                <input v-model="formTaskTime" type="number" id="taskTime" class="form-control" required>
              </div>

              <button type="submit" class="btn btn-success">Add Task</button>
            </form>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
      </div>
    </div>

  </div>
</div>
</template>

<style>
/* Add your additional styles here if needed */
</style>
