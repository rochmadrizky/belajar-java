<template>
  <div>
    <h1 class="my-4 text-center text-2xl">Tugas perulangan 1-10</h1>
    <div class="flex items-center justify-center">
      <div v-for="perulanganAngka in angka" :key="perulanganAngka" class="mr-2">
        {{ perulanganAngka }}
      </div>
    </div>
    <!--  -->
    <h1 class="my-4 text-center text-2xl">Daftar Buah</h1>
    <ul>
      <li
        v-for="(iniBuah, index) in buah"
        :key="index"
        class="flex items-center justify-center"
      >
        {{ iniBuah }}
      </li>
    </ul>
    <p class="mt-4 text-center" v-if="buah.length >= 3">
      Buah Ketiga: {{ buah[2] }}
    </p>
    <!--  -->
    <h1 class="my-4 text-center text-2xl">Penjumlahan dan Pengurangan</h1>
    <p class="text-center">
      Hasil Penjumlahan 5 + 7 : {{ penjumlahanAngka(5, 7) }}
    </p>
    <p class="text-center">
      Hasil Pengurangan 10 - 3 : {{ penguranganAngka(10, 3) }}
    </p>
    <!--  -->
    <h1 class="my-4 text-center text-2xl">Informasi Data Orang</h1>
    <pre class="text-center" v-text="objectKu" />
    <p class="text-center">dia berumur {{ objectKu.umur }}</p>
    <!--  -->
    <div class="my-4 flex items-center justify-center">
      <button
        @click="cobaKlik"
        class="bg-blue-500 text-white px-4 py-2 rounded"
      >
        Coba
      </button>
    </div>
  </div>
</template>

<script setup>
const angka = Array.from({ length: 10 }, (_, index) => index + 1);

const buah = ref(["Apel", "Jeruk", "Pisang", "Anggur"]);

const penjumlahanAngka = (num1, num2) => {
  return num1 + num2;
};

const penguranganAngka = (num1, num2) => {
  return num1 - num2;
};

const objectKu = ref({
  nama: "Sobirin",
  umur: 29,
  kota: "Surabaya",
});

const cobaKlik = () => {
  console.log("Tombol diklik!");
};
</script>
