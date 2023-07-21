<script>
import "@patternfly/pfe-card";
import "@patternfly/pfe-cta";
import "@patternfly/pfe-button";
import "@patternfly/pfe-tabs";
import { ref } from "vue";
// import ActiveTask from "./components/ActiveTask.vue";
// import ClosedTask from "./components/ActiveTask.vue";

export default {
  // components: {
  //   ActiveTask,
  //   ClosedTask,
  // },
  setup() {
    const newTodo = ref("");
    const checkBox = ref(false);
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
      checkBox,
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
          class="userinput"
          type="text"
          placeholder="Enter your task"
          v-model="newTodo"
        />
        <pfe-button>
          <button class="addbutton" @click="addnewTodo">Add</button>
        </pfe-button>
      </div>
      <div class="card-tabs">
        <pfe-tabs variant="earth" tab-align="center" @click="show">
          <pfe-tab role="heading" slot="tab">
            <h1>Active Tasks</h1>
          </pfe-tab>
          <pfe-tab-panel role="region" slot="panel" class="tab-panel-body">
            <div class="main-list-body">
              <li
                v-for="(todo, index) in todos"
                :key="todo.id"
                class="task-list"
                style="list-style: none"
              >
                <div class="todo-data">
                  <input
                    type="checkbox"
                    v-model="checkBox"
                    @click="checkToDO(index, event)"
                    class="checkbox-input"
                    :id="'checkbox' + index"
                  />
                  <h3>{{ todo.content }}</h3>
                  <h4>{{ todo.id }}</h4>
                </div>
              </li>
            </div>
          </pfe-tab-panel>
          <pfe-tab role="heading" slot="tab">
            <h1>Closed Tasks</h1>
          </pfe-tab>
          <pfe-tab-panel role="region" slot="panel" class="tab-panel-body">
            <ol type="1">
              <li
                v-for="(todo, index) in completedTodo"
                :key="todo.id"
                class="task-list"
              >
                <h3>{{ todo.content }}</h3>
              </li>
            </ol>
          </pfe-tab-panel>
        </pfe-tabs>
      </div>
    </pfe-card>
  </div>
</template>

<style src="./style.css"></style>
