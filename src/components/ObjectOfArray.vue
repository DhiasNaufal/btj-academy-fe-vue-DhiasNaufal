<template>
  <div class="flex flex-col items-center min-h-screen pt-11">
    <h1 class="text-left">TODO APP - Object Of Arrays</h1>

    <div class="sm:w-3/5 w-11/12 flex flex-col gap-5">
      <div class="sm:flex gap-3 w-full items-start text-start hidden xxl:flex">
        <div
          v-for="(item, index) in priorities"
          :key="index"
          class="border border-gray-500 rounded p-3 flex flex-col"
        >
          <h1 class="text-center">{{ item.title }}</h1>
          <p class="text-center">{{ item.value }}</p>
        </div>
      </div>
      <div class="border border-gray-500 rounded p-3 w-full sm:px-11">
        <form
          id="form"
          @submit.prevent="tambah"
          class="sm:flex gap-5 items-end"
        >
          <div class="flex flex-col sm:w-1/2">
            <label for="nama">Nama</label>
            <input
              type="text"
              name="nama"
              id="nama"
              v-model="nama"
              class="border border-gray-500 h-[40px] p-1"
            />
          </div>
          <div class="flex flex-col sm:w-1/2">
            <label for="priority">Priority</label>
            <select
              name="priority"
              id="priority"
              v-model="priority"
              class="border border-gray-500 h-[40px] p-1"
            >
              <option v-for="(item, index) in priorityList" :value="item">
                {{ item }}
              </option>
            </select>
          </div>
          <button
            type="submit"
            class="bg-green-600 text-white px-2 flex h-[40px] items-center rounded-lg shadow-sm w-full sm:w-[100px] justify-center mt-2"
          >
            Tambah
          </button>
        </form>
      </div>

      <div class="flex sm:flex-row flex-col w-full gap-2">
        <div class="flex flex-col sm:w-1/2 w-full justify-start">
          <h1 class="font-bold">TO-DO</h1>
          <div v-for="(item, index) in todoList" :key="index">
            <div
              v-if="item.status === false"
              class="flex flex-col justify-between border border-gray-600 p-4 rounded my-1 h-[90px]"
            >
              <h1 class="text-lg font-semibold">{{ item.nama }}</h1>
              <div class="flex justify-between">
                <div class="flex gap-1 items-center">
                  <div
                    class="w-[15px] h-[15px] rounded"
                    :class="{
                      'bg-blue-500': item.priority === 'Low',
                      'bg-red-500': item.priority === 'High',
                      'bg-yellow-500': item.priority === 'Medium',
                    }"
                  ></div>
                  {{ item.priority }}
                </div>
                <div class="flex gap-2">
                  <button
                    @click="hapus(index)"
                    class="bg-red-600 text-white rounded-xl py-1 px-3 shadow-sm"
                  >
                    Hapus
                  </button>
                  <button
                    @click="selesai(index)"
                    class="bg-green-600 text-white rounded-xl py-1 px-3 shadow-sm"
                  >
                    Selesai
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="flex flex-col sm:w-1/2">
          <h1 class="font-bold">DONE</h1>
          <div v-for="(item, index) in todoList" :key="index">
            <div
              v-if="item.status == true"
              class="flex flex-col justify-between border border-gray-500 p-4 rounded my-1 h-[90px]"
            >
              <h1 class="text-lg font-semibold">{{ item.nama }}</h1>
              <div class="flex justify-between">
                <div class="flex gap-1 items-center">
                  <div
                    class="w-[15px] h-[15px] rounded"
                    :class="{
                      'bg-blue-500': item.priority === 'Low',
                      'bg-red-500': item.priority === 'High',
                      'bg-yellow-500': item.priority === 'Medium',
                    }"
                  ></div>
                  {{ item.priority }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div>{{ todoList }}</div>
</template>

<script>
export default {
  data() {
    return {
      priorityList: ["Low", "Medium", "High"],
      nama: null,
      priority: null,
      status: false,
      todoList: [],
    };
  },
  methods: {
    tambah() {
      if (this.nama == null && this.priority !== null) {
        alert("Nama TodoList tidak boleh kosong");
      } else if (this.nama !== null && this.priority == null) {
        alert("Pririty tidak boleh kosong");
      } else if (this.nama !== null && this.priority !== null) {
        this.todoList.push({
          nama: this.nama,
          priority: this.priority,
          status: this.status,
        });
        this.nama = null;
        this.priority = null;
      } else {
        alert("Nama TodoList and Priority tidak boleh kosong");
      }
    },

    selesai(index) {
      this.todoList[index].status = true;
    },

    hapus(index) {
      this.todoList.splice(index, 1);
    },
  },
  computed: {
    totalPending() {
      return this.todoList.filter((item) => item.status === false).length;
    },
    totalDone() {
      return this.todoList.filter((item) => item.status === true).length;
    },
    totalLow() {
      return this.todoList.filter(
        (item) => item.status === false && item.priority === "Low"
      ).length;
    },
    totalMed() {
      return this.todoList.filter(
        (item) => item.status === false && item.priority === "Medium"
      ).length;
    },
    totalHigh() {
      return this.todoList.filter(
        (item) => item.status === false && item.priority === "High"
      ).length;
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
