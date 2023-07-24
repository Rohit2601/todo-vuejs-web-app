<script>
import { ref } from "vue";
export default {
  props: {
    todos: Array,
    checkToDO: Function,
  },
};
</script>

<template>
  <pfe-tab-panel role="region" slot="panel" class="tab-panel-body">
    <div class="main-list-body">
      <li
        v-for="(todo, index) in todos"
        :key="todo"
        class="task-list"
        style="list-style: none"
      >
        <div class="todo-data">
          <input
            type="checkbox"
            @click="checkToDO(index, event)"
            class="checkbox-input"
            :id="'checkbox' + index"
          />
          <hr />
          <h3>{{ todo.content }}</h3>
          <hr />
          <h4>{{ todo.id }}</h4>
        </div>
      </li>
    </div>
  </pfe-tab-panel>
</template>
