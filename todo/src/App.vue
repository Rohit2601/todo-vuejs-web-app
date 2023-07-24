<script>
import "@patternfly/pfe-card";
import "@patternfly/pfe-cta";
import "@patternfly/pfe-button";
import "@patternfly/pfe-tabs";
import { ref } from "vue";
import ActiveTask from "./components/ActiveTask.vue";
import ClosedTask from "./components/ClosedTask.vue";

export default {
  components: {
    ActiveTask,
    ClosedTask,
  },
  setup() {
    const newTodo = ref("");
    const todos = ref([]);
    const completedTodo = ref([]);
    const allToDo = ref([]);

    function addnewTodo() {
      if (newTodo.value == "") {
        alert("Add something");
      } else {
        todos.value.push({
          done: false,
          content: newTodo.value,
          id: new Date(new Date().getTime()).toLocaleDateString("en-US"),
        });
        newTodo.value = "";
      }
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function checkToDO(index, event) {
      console.log(event);
      completedTodo.value.push(todos.value[index]);
      todos.value.splice(index, 1);
    }

    return {
      todos,
      newTodo,
      addnewTodo,
      removeTodo,
      checkToDO,
      completedTodo,
    };
  },
};
</script>

<template>
  <div class="app-body">
    <div class="signin">
      <pfe-button class="signup-button" variant="danger">
        <button>Sign Up</button>
      </pfe-button>
      <pfe-button variant="danger">
        <button>Log in</button>
      </pfe-button>
    </div>

    <h1 class="heading">ToDo App using VueJs</h1>
    <pfe-card class="pfe-card">
      <div class="form_card">
        <input
          class="user-input"
          type="text"
          placeholder="Enter your task"
          v-model="newTodo"
        />
        <pfe-button>
          <button class="add-button" @click="addnewTodo">Add</button>
        </pfe-button>
      </div>
      <div class="card-tabs">
        <pfe-tabs variant="earth" tab-align="center" @click="show">
          <pfe-tab role="heading" slot="tab">
            <h1>Active Tasks</h1>
          </pfe-tab>
          <ActiveTask :todos="todos" :checkToDO="checkToDO"></ActiveTask>
          <pfe-tab role="heading" slot="tab">
            <h1>Closed Tasks</h1>
          </pfe-tab>
          <ClosedTask :completedTodo="completedTodo"></ClosedTask>
        </pfe-tabs>
      </div>
    </pfe-card>
  </div>
</template>

<style src="./style.css"></style>
