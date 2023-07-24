<script>
import { ref } from "vue";
export default {
  props: {
    completedTodo: {
      type: Array,
    }
  }
};
</script>

<template>
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
</template>
