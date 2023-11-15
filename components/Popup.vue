<template>
  <div class="relative">
    <div
      v-if="bukaDropdown"
      class="fixed inset-0 bg-black opacity-50"
      @click="tutupBackdrop"
    ></div>

    <div class="max-w-2xl mx-auto">
      <div class="flex items-center justify-center">
        <button
          @click="tombolDropdown"
          class="bg-black text-white font-bold py-2 px-4 rounded"
        >
          Jenis Hewan

          <div
            v-show="bukaDropdown"
            class="absolute mt-2 bg-white border rounded-lg shadow-lg"
          >
            <button
              @click="tampilkanJenisHewan('darat')"
              class="block w-full text-left px-4 py-2 text-black hover:bg-gray-100"
            >
              Darat
            </button>
            <button
              @click="tampilkanJenisHewan('air')"
              class="block w-full text-left px-4 py-2 text-black hover:bg-gray-100"
            >
              Air
            </button>
            <button
              @click="tampilkanJenisHewan('udara')"
              class="block w-full text-left px-4 py-2 text-black hover:bg-gray-100"
            >
              Udara
            </button>
          </div>
        </button>

        <div
          v-if="bukaPopUp"
          class="fixed inset-0 flex items-center justify-center"
        >
          <div
            v-if="bukaPopUp"
            class="fixed inset-0 bg-blue-600 opacity-50"
            @click="bukaPopUp = false"
          ></div>
          <div class="bg-white p-6 rounded-lg z-10">
            <p class="text-lg font-bold mb-4">
              Nama Hewan: {{ kumpulanHewan.join(", ") }}
            </p>
            <button
              @click="tutupPopUp"
              class="bg-red-500 text-white font-bold py-2 px-4 rounded"
            >
              Tutup
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const bukaPopUp = ref(false);
const kumpulanHewan = ref([]);
const bukaDropdown = ref(false);

const tombolDropdown = () => {
  bukaDropdown.value = !bukaDropdown.value;
};

const tampilkanJenisHewan = (type) => {
  kumpulanHewan.value = [];

  if (type === "darat") {
    kumpulanHewan.value.push("Kucing", "Sapi", "Kambing");
  } else if (type === "air") {
    kumpulanHewan.value.push("Ikan", "Kepiting", "Belut");
  } else if (type === "udara") {
    kumpulanHewan.value.push("Elang", "Merpati", "Kelelawar");
  }

  bukaPopUp.value = true;
};

const tutupPopUp = () => {
  bukaPopUp.value = false;
};

const tutupBackdrop = () => {
  bukaDropdown.value = false;
  bukaPopUp.value = false;
};
</script>
