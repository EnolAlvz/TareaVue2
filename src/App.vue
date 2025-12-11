<template>
  <div class="container">
    <h1>Administrador de Tareas</h1>

    <!-- Crear tarea -->
    <form @submit.prevent="addTask" class="task-form">
      <input
        v-model="newTask"
        type="text"
        placeholder="Nueva tarea..."
        required
      />
      <button>Agregar</button>
    </form>

    <!-- Lista de tareas -->
    <ul class="task-list">
      <li v-for="task in tasks" :key="task.id">
        <label>
          <input type="checkbox" v-model="task.done" />
          <span :class="{ done: task.done }">{{ task.text }}</span>
        </label>
        <button class="delete-btn" @click="removeTask(task.id)">❌</button>
      </li>
    </ul>

    <p v-if="tasks.length === 0">No hay tareas aún.</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: "",
      tasks: [],
    };
  },

  methods: {
    addTask() {
      this.tasks.push({
        id: Date.now(),
        text: this.newTask,
        done: false,
      });
      this.newTask = "";
    },

    removeTask(id) {
      this.tasks = this.tasks.filter((t) => t.id !== id);
    },
  },
};
</script>

<style>
body {
  background: #f5f5f5;
  margin: 0;
  font-family: Arial;
}

.container {
  max-width: 500px;
  margin: 40px auto;
  padding: 20px;
  background: white;
  border-radius: 8px;
  box-shadow: 0 3px 8px rgba(0, 0, 0, 0.1);
}

h1 {
  text-align: center;
}

.task-form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.task-form input {
  flex: 1;
  padding: 10px;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-list li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px 0;
  border-bottom: 1px solid #ddd;
}

.done {
  text-decoration: line-through;
  color: gray;
}

.delete-btn {
  background: transparent;
  border: none;
  cursor: pointer;
  font-size: 18px;
}
</style>
