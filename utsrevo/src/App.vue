<script setup>
import { ref, computed } from 'vue';

const newTask = ref('');
const tasks = ref([]);
const showUnfinishedOnly = ref(false);

const addTask = () => {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value.trim(), done: false });
    newTask.value = '';
  }
};

const removeTask = (index) => {
  tasks.value.splice(index, 1);
};

const filteredTasks = computed(() => {
  return showUnfinishedOnly.value
    ? tasks.value.filter((task) => !task.done)
    : tasks.value;
});
</script>


<template>
  <div class="app">
    <img src="https://upload.wikimedia.org/wikipedia/en/4/47/FC_Barcelona_%28crest%29.svg" alt="FC Barcelona Logo" class="logo" />

    <h1 class="title">Daftar Pemain Barca</h1>
    <div class="form">
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Tambahkan kegiatan" />
      <button @click="addTask">Tambah</button>
    </div>

    <div class="filter">
      <label>
        <input type="checkbox" v-model="showUnfinishedOnly" /> Tampilkan Pemain Yang Belum Latihan
      </label>
    </div>

    <ul>
      <li v-for="(task, index) in filteredTasks" :key="index">
        <input type="checkbox" v-model="task.done" />
        <span :class="{ done: task.done }">{{ task.text }}</span>
        <button @click="removeTask(index)">Batal</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.logo {
  display: block;
  margin: 0 auto 10px auto;
  width: 80px;
  animation: bounceIn 1s ease;
}

@keyframes bounceIn {
  0% {
    transform: scale(0.5);
    opacity: 0;
  }
  60% {
    transform: scale(1.1);
    opacity: 1;
  }
  100% {
    transform: scale(1);
  }
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 5px;
  margin-bottom: 8px;
  animation: fadeIn 0.5s ease;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}

.app {
  max-width: 500px;
  margin: 50px auto;
  padding: 20px;
  border-radius: 15px;
  background: linear-gradient(to bottom right, #a50044, #004d98); /* Barcelona colors */
  color: #fff;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
}

.title {
  text-align: center;
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 20px;
  color: gold;
  text-shadow: 1px 1px 2px #000;
}

.form input {
  width: 70%;
  padding: 8px;
  margin-right: 10px;
  border-radius: 5px;
  border: none;
}

.form button {
  padding: 8px 16px;
  background-color: gold;
  color: #000;
  border: none;
  border-radius: 5px;
  font-weight: bold;
  cursor: pointer;
}

.filter {
  margin: 10px 0;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 5px;
  margin-bottom: 8px;
}

.done {
  text-decoration: line-through;
  opacity: 0.7;
}

button {
  margin-left: 10px;
  color: #fff;
  background-color: transparent;
  border: none;
  cursor: pointer;
}
</style>