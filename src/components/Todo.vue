<template>
  <input type="text" v-model="newTask" @keyup.enter="addTask" />
  <p v-if="isVisible">Este es un parrafo que quiero ocultar</p>
  <p v-else>
    Este es el parrafo que quiero mostrar cuando el primero se oculta
  </p>
  <div class="flex space-between">
    <p>Total de Tareas: {{ numberOfTasks }}</p>
    <p>Tareas completadas: {{ tasksCompleted }}</p>
    <p>Tareas incompletas: {{ pendingTasks }}</p>
  </div>
  <ul>
    <TodoItem
      :class="{ 'margin-15': isDesktop }"
      :task="task"
      v-for="task in tasks"
      :key="task.id"
      :completeTask="completeTask"
    />
  </ul>
</template>
<script>
import {
  computed,
  onBeforeUnmount,
  onMounted,
  ref,
  watch,
  watchEffect,
} from "vue";
import { v4 as uuidv4 } from "uuid";
import TodoItem from "./TodoItem.vue";

export default {
  name: "Todo",
  components: {
    TodoItem,
  },
  setup() {
    const tasks = ref([]);
    const newTask = ref("");

    // lifecycle
    onMounted(() => {
      console.log("mounted");
      const initialTasks = [
        {
          id: uuidv4(),
          task: "Crear curso de EDteam",
          isCompleted: true,
        },
        {
          id: uuidv4(),
          task: "Revisar comentarios del curso",
          isCompleted: false,
        },
        {
          id: uuidv4(),
          task: "Grabar nuevas secciones",
          isCompleted: false,
        },
        {
          id: uuidv4(),
          task: "Modificar secciones anteriores",
          isCompleted: false,
        },
      ];
      tasks.value = initialTasks;
    });

    onBeforeUnmount(() => {
      console.log("BeforeUnmount");
    });

    // methods
    const addTask = () => {
      tasks.value.push({
        id: uuidv4(),
        task: newTask.value,
        isCompleted: false,
      });
      newTask.value = "";
    };

    const completeTask = (task) => {
      //let taskSelected = tasks.value.filter(t => t.id === task.id);
      task.isCompleted = true;
    };

    // computed properties
    const numberOfTasks = computed(() => {
      return tasks.value.length;
    });

    const tasksCompleted = computed(() => {
      const completedTasks = tasks.value.filter((task) => {
        return task.isCompleted === true;
      });
      return completedTasks.length;
    });

    const pendingTasks = computed(() => {
      const pending = tasks.value.filter((task) => {
        return task.isCompleted === false;
      });
      return pending.length;
    });

    // watchers
    watchEffect(() => console.log(tasks.value));

    watch(newTask, (current, prev) => {
      console.log(current);
      console.log(prev);
    });

    return {
      tasks,
      newTask,
      numberOfTasks,
      tasksCompleted,
      pendingTasks,
      addTask,
      completeTask,
      isVisible: ref(true),
      activeColor: ref("#fff"),
      background: ref("green"),
      fontSize: ref(16),
      isDesktop: ref(true),
    };
  },
};
</script>
<style>
.flex {
  display: flex;
  max-width: 500px;
  margin: auto;
}
.space-between {
  justify-content: space-between;
}
</style>