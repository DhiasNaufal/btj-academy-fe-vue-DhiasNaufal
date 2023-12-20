<template>
  <h1>TODO APP</h1>
  <!-- <div id="sumamary" class="flex gap-2">
    <ul v-for="(item, index) in status">
      <li>{{ item }}</li>
    </ul>
  </div> -->
  <p>{{ totalPending }} - pending</p>
  <p>{{ totalDone }}- selese</p>
  <p>{{ totalLow }}- low</p>
  <p>{{ totalMed }}-med</p>
  <p>{{ totalHigh }}-high</p>
  <form id="form" @submit.prevent="tambah">
    <label for="nama">Nama</label>
    <input type="text" name="nama" id="nama" v-model="nama" />
    <label for="priority">Priority</label>
    <select name="priority" id="priority" v-model="priority">
      <option v-for="(item, index) in priorityList" :value="item.toLowerCase()">
        {{ item.toLowerCase() }}
      </option>
    </select>
    <button type="submit">Tambah</button>
  </form>
  <div id="list">
    <ul>
      <!-- <li v-for="(item, index) in listNama" :key="index">{{ item }}</li> -->
    </ul>
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
  },
};
</script>
<style></style>
