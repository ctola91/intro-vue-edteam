<template>
  <li :class="{ done: task.isCompleted }">
    {{ task.task }}
    <button @click="completeTask(task)" v-show="!task.isCompleted">
      Completar
    </button>
  </li>
</template>
<script>
export default {
  name: "TodoItem",
  props: ["task", "completeTask"],
  setup() {},
};
</script>
<style>
li {
  list-style: none;
}
.done {
  color: #ffffff;
  background: #3eaf7c;
  font-size: 16px;
}
</style>