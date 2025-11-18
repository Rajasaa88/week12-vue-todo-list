<script setup>
import { ref } from 'vue'

const newTask = ref('')
const tasks = ref([])

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value) // Tambah ke array
    newTask.value = '' // Reset input jadi kosong
  }
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1) // Hapus 1 item berdasarkan index
}
</script>

<template>
  <div class="container">
    <h1>To-Do List Tugas 4</h1>
    
    <form @submit.prevent="addTask" class="input-group">
      <input 
        v-model="newTask" 
        type="text" 
        placeholder="Tambahkan tugas baru..." 
      />
      <button type="submit">Tambah</button>
    </form>

    <p v-if="tasks.length === 0" class="empty-msg">
      Tidak ada tugas
    </p>

    <ul v-else>
      <li v-for="(task, index) in tasks" :key="index">
        <span>{{ task }}</span>
        <button @click="deleteTask(index)" class="delete-btn">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
/* Styling agar tampilan rapi sesuai permintaan */
.container {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-family: Arial, sans-serif;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

h1 {
  text-align: center;
  color: #333;
}

.input-group {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 8px 12px;
  background-color: #42b883; /* Warna khas Vue */
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #33a06f;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #f9f9f9;
  margin-bottom: 8px;
  padding: 10px;
  border-radius: 4px;
  border-bottom: 1px solid #eee;
}

.delete-btn {
  background-color: #ff4d4d;
  font-size: 0.8em;
}

.delete-btn:hover {
  background-color: #cc0000;
}

.empty-msg {
  text-align: center;
  color: #888;
  font-style: italic;
}
</style>