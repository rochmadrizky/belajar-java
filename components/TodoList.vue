<template>
  <div class="mt-4 max-w-md mx-auto bg-gray-400 p-6 rounded shadow-lg">
    <h1 class="text-2xl font-semibold text-center">List Task</h1>
    <p class="text-center">Add your assignment below</p>
    <div class="my-4">
      <input
        v-if="editIndex === -1"
        v-model="tugasBaru"
        type="text"
        class="w-full p-2 bg-gray-200 border rounded"
        placeholder="Add notes here..."
        @keyup.enter="tambahkanTugasBaru"
      />

      <div class="pt-6 flex items-center justify-center">
        <button
          @click="tambahkanTugasBaru"
          class="text-white py-2 px-4 rounded"
          :class="{
            'bg-gray-500 cursor-not-allowed':
              tugasBaru.trim() === '' || editIndex !== -1,
            'bg-blue-500': tugasBaru.trim() !== '' && editIndex === -1,
          }"
          :disabled="tugasBaru.trim() === '' || editIndex !== -1"
        >
          Tambahkan
        </button>
      </div>
    </div>
  </div>

  <div class="my-6 max-w-md mx-auto bg-gray-400 p-6 rounded shadow-lg">
    <h1 class="text-2xl font-semibold text-center">
      Task list that you have created
    </h1>
    <p class="text-center">The task list you created will be displayed here</p>
    <ul class="my-4">
      <li
        v-for="(task, index) in tugas"
        :key="index"
        :class="{
          'bg-green-500': task.completed,
          'bg-white': !task.completed,
        }"
        class="flex justify-between items-center w-full p-2 border rounded"
      >
        <div class="flex items-center">
          <input
            type="checkbox"
            @change="centangCheckbox"
            v-model="tugas[index].completed"
            class="mr-2"
          />
          <span v-if="editIndex !== index" class="flex items-center"
            >{{ task.isi }}
            <button @click="mulaiEdit(index)" class="ml-2 opacity-70">
              <IconPencil />
            </button>
          </span>

          <input
            v-else
            v-model="tugasBaru"
            @keyup.enter="selesaiEdit"
            @keyup.esc="batalEdit"
            class="w-full p-1 border rounded"
          />
        </div>

        <button
          @click="hapusTugasTunggal(index)"
          :disabled="!tugas.length || editIndex !== -1"
          class="opacity-70"
        >
          <IconTrash />
        </button>
      </li>

      <p
        v-if="tugas.length === 0"
        class="w-full p-2 border rounded bg-gray-200 text-center text-gray-400"
      >
        There is no set of notes
      </p>
    </ul>

    <div class="flex items-center justify-center mt-4 gap-6">
      <button
        @click="tombolSemuaSelelsai"
        :disabled="!tugas.length || editIndex !== -1"
        :class="[
          tugas.length && editIndex === -1
            ? 'bg-green-500'
            : 'bg-gray-500 cursor-not-allowed',
        ]"
        class="py-2 px-4 text-white rounded"
      >
        Selesai semua
      </button>

      <button
        @click="notifHapusSemuaTugas"
        @keyup.enter="konfirmasiHapusSemuaTugas"
        :disabled="!tugas.length || editIndex !== -1"
        :class="[
          tugas.length && editIndex === -1
            ? 'bg-red-500'
            : 'bg-gray-500 cursor-not-allowed',
        ]"
        class="py-2 px-4 text-white rounded"
      >
        Hapus Semua
      </button>
    </div>
  </div>
</template>

<script setup>
import { IconTrash } from "@tabler/icons-vue";
import { IconPencil } from "@tabler/icons-vue";

const tugas = ref([]);
const tugasBaru = ref("");
const editIndex = ref(-1);

const localStorageUntukTugas = "toDoTugas";

const simpanTugasKeLocalStorage = () => {
  localStorage.setItem(localStorageUntukTugas, JSON.stringify(tugas.value));
};

const loadTugasDalamLocalStorage = () => {
  const simpanTugas = localStorage.getItem(localStorageUntukTugas);
  if (simpanTugas) {
    tugas.value = JSON.parse(simpanTugas);
  }
};

onMounted(() => {
  loadTugasDalamLocalStorage();
});

const tambahkanTugasBaru = () => {
  if (tugasBaru.value.trim() !== "") {
    tugas.value.push({ isi: tugasBaru.value, completed: false });
    tugasBaru.value = "";
    simpanTugasKeLocalStorage();
  }
};

const mulaiEdit = (index) => {
  editIndex.value = index;
  tugasBaru.value = tugas.value[index].isi;
};

const centangCheckbox = () => {
  simpanTugasKeLocalStorage();
};

const selesaiEdit = () => {
  if (editIndex.value !== -1 && tugasBaru.value.trim() !== "") {
    tugas.value[editIndex.value].isi = tugasBaru.value;
    editIndex.value = -1;
    tugasBaru.value = "";
    simpanTugasKeLocalStorage();
  }
};

const batalEdit = () => {
  editIndex.value = -1;
  tugasBaru.value = "";
};

const semuaTugasSelesai = computed(() =>
  tugas.value.every((task) => task.completed)
);

const hapusTugas = (index) => {
  tugas.value.splice(index, 1);
  simpanTugasKeLocalStorage();
};

const tombolSemuaSelelsai = () => {
  if (!semuaTugasSelesai.value) {
    tugas.value.forEach((task) => {
      task.completed = true;
    });
  }
  simpanTugasKeLocalStorage();
};

const notifHapusSemuaTugas = () => {
  if (confirm("Yakin dihapus semua?")) {
    hapusSemuaTugas();
  }
};

const hapusTugasTunggal = (index) => {
  const taskText = tugas.value[index].isi;
  if (confirm(`Yakin ${taskText} dihapus?`)) {
    hapusTugas(index);
  }
};

const hapusSemuaTugas = () => {
  tugas.value = [];
  simpanTugasKeLocalStorage();
};
</script>
