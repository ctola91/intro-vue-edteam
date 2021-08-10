<template>
  <input type="text" v-model="newTask" />
  <p v-if="isVisible">Este es un parrafo que quiero ocultar</p>
  <p v-else>
    Este es el parrafo que quiero mostrar cuando el primero se oculta
  </p>
  <ul>
    <li
      :key="task.id"
      :class="{ 'margin-15': isDesktop }"
      v-for="task in tasks"
      :style="{
        color: activeColor,
        background: background,
        fontSize: fontSize + 'px',
      }"
    >
      {{ task.task }}
    </li>
  </ul>
</template>
<script>
export default {
  name: "Todo",
  data() {
    return {
      tasks: [
        {
          id: 1,
          task: "Crear curso de EDteam",
          isCompleted: false,
        },
        {
          id: 2,
          task: "Revisar comentarios del curso",
          isCompleted: false,
        },
        {
          id: 3,
          task: "Grabar nuevas secciones",
          isCompleted: false,
        },
        {
          id: 4,
          task: "Modificar secciones anteriores",
          isCompleted: false,
        },
      ],
      newTask: "",
      isVisible: true,
      activeColor: "#fff",
      background: "green",
      fontSize: 16,
      isDesktop: true,
    };
  },
};
</script>
