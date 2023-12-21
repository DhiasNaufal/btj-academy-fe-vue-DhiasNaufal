<template>
  <h1>TODO APP</h1>
  <div class="flex gap-3">
    <div class="border border-gray-500 rounded p-3">
      <h1 class="text-center">PENDING</h1>
      <p class="text-center">{{ totalPending }}</p>
    </div>
    <div>
      <h1>LOW PRIORITY</h1>
      <p class="text-center">{{ totalLow }}</p>
    </div>
    <div>
      <h1>MEDIUM PRIORITY</h1>
      <p class="text-center">{{ totalMed }}</p>
    </div>
    <div>
      <h1>HIGH PRIORITY</h1>
      <p class="text-center">{{ totalHigh }}</p>
    </div>
    <div>
      <h1>FINISHED</h1>
      <p class="text-center">{{ totalDone }}</p>
    </div>
  </div>

  <form id="form" @submit.prevent="tambah">
    <label for="nama">Nama</label>
    <input type="text" name="nama" id="nama" v-model="nama" />
    <label for="priority">Priority</label>
    <select name="priority" id="priority" v-model="priority" class="">
      <option v-for="(item, index) in priorityList" :value="item.toLowerCase()">
        {{ item.toLowerCase() }}
      </option>
    </select>
    <button type="submit">Tambah</button>
  </form>
  <div id="list">
    <ul></ul>
  </div>
  <!-- <p>{{ nama }}</p> -->
  <div class="flex">
    <div class="flex flex-col">
      <div v-for="(item, index) in todoList.nama" :key="index">
        <ul v-if="todoList.status[index] == false">
          <li>
            {{ item }} - {{ todoList.priority[index] }} -
            {{ todoList.status[index] }}
          </li>
          <button @click="selesai(index)">done</button>
          <button on @click="hapus(index)">Hapus</button>
          <div
            :class="{
              'bg-blue-500': todoList.priority[index] === 'low',
              'bg-red-500': todoList.priority[index] === 'high',
              'bg-yellow-500': todoList.priority[index] === 'medium',
            }"
          >
            sdad
          </div>
        </ul>
      </div>
    </div>
    <div class="flex flex-col">
      <div v-for="(item, index) in todoList.nama" :key="index">
        <ul v-if="todoList.status[index] == true">
          <li>
            {{ item }} - {{ todoList.priority[index] }} -
            {{ todoList.status[index] }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      priorityList: ["Low", "Medium", "High"],
      nama: null,
      priority: null,
      status: false,
      todoList: {
        nama: [],
        priority: [],
        status: [],
      },
      aselole: [],
    };
  },
  methods: {
    tambah() {
      this.todoList.nama.push(this.nama);
      this.todoList.priority.push(this.priority);
      this.todoList.status.push(this.status);
      this.nama = null;
      this.priority = null;
    },
    selesai(index) {
      this.todoList.status[index] = true;
    },
    hapus(index) {
      this.todoList.nama.splice(index, 1);
      this.todoList.priority.splice(index, 1);
      this.todoList.status.splice(index, 1);
    },
  },
  computed: {
    totalPending() {
      let total = 0; // Initialize total as a number
      for (let i = 0; i < this.todoList.nama.length; i++) {
        if (this.todoList.status[i] === false) {
          total++;
        }
      }
      return total;
    },
    totalDone() {
      let total = 0; // Initialize total as a number
      for (let i = 0; i < this.todoList.nama.length; i++) {
        if (this.todoList.status[i] === true) {
          total++;
        }
      }
      return total;
    },
    totalLow() {
      let total = 0; // Initialize total as a number
      for (let i = 0; i < this.todoList.nama.length; i++) {
        if (this.todoList.priority[i] === "low") {
          total++;
        }
      }
      return total;
    },
    totalMed() {
      let total = 0; // Initialize total as a number
      for (let i = 0; i < this.todoList.nama.length; i++) {
        if (this.todoList.priority[i] === "medium") {
          total++;
        }
      }
      return total;
    },
    totalHigh() {
      let total = 0; // Initialize total as a number
      for (let i = 0; i < this.todoList.nama.length; i++) {
        if (this.todoList.priority[i] === "high") {
          total++;
        }
      }
      return total;
    },
    priorities() {
      return [
        { title: "PENDING", value: this.totalPending },
        { title: "LOW PRIORITY", value: this.totalLow },
        { title: "MEDIUM PRIORITY", value: this.totalMed },
        { title: "HIGH PRIORITY", value: this.totalHigh },
        { title: "FINISHED", value: this.totalDone },
      ];
    },
  },
};
</script>
<style></style>
