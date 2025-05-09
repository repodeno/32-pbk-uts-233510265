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
</style>
