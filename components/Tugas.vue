<template>
  <div class="flex items-center justify-center">
    <div>
      <!-- 1&2 -->
      <h1 class="text-2xl font-bold my-4">1&2. Daftar Belanja</h1>
      <ul>
        <li v-for="item in daftarBelanja" :key="item" class="text-center">
          {{ item }}
        </li>
      </ul>

      <!-- 3 -->
      <h1 class="text-2xl font-bold my-4">3. Angka Genap</h1>
      <p>Sebelum difilter: {{ arrayAwal }}</p>
      <p>Setelah Filter: {{ arrayGenap }}</p>

      <!-- 4 -->
      <h1 class="text-2xl font-bold my-4">4. Cari Kata</h1>
      <p>Array Kata: {{ arrayKata }}</p>
      <p>"jeruk": {{ cariBuah("jeruk") }}</p>
      <p>"apel": {{ cariBuah("apel") }}</p>
      <p>"pisang": {{ cariBuah("pisang") }}</p>
      <p>"anggur": {{ cariBuah("anggur") }}</p>

      <!-- 5 -->
      <h1 class="text-2xl font-bold my-4">5. Cari kata buah</h1>
      <input
        v-model="cariKata"
        class="border p-2 mb-4"
        placeholder="Masukkan kata"
        @keyup="cari"
      />
      <button @click="cari" class="bg-blue-500 text-white px-4 py-2 rounded">
        Cari
      </button>

      <div v-if="hasilDitemukan !== -1" class="mt-4 text-green-500">
        Kata '{{ cariKata }}' ditemukan dalam array pada indeks:
        {{ hasilDitemukan }}
      </div>
      <div v-else-if="cariKata !== ''" class="mt-4 text-red-500">
        Kata '{{ cariKata }}' tidak ditemukan dalam array.
      </div>

      <!-- 6 -->
      <h1 class="text-2xl font-bold my-4">6. Tic Tac Toe</h1>
      <div class="grid grid-row-3 mb-4">
        <div v-for="(urutan, index) in ticTacToe" :key="index" class="flex">
          <div
            v-for="(hasil, barisanIndex) in urutan"
            :key="barisanIndex"
            class="w-12 h-12 border flex items-center justify-center"
          >
            {{ hasil }}
          </div>
        </div>
      </div>

      <!-- 7 -->
      <h1 class="text-2xl font-bold my-4">7. Gabungkan Array</h1>
      <ul class="flex items-center justify-center mb-4 gap-2">
        <li v-for="item in arrayBaru" :key="item" class="text-lg mb-2">
          {{ item }}
        </li>
      </ul>

      <!-- 8 -->
      <h1 class="text-2xl font-bold my-4">8. Sorting Component</h1>
      <div>
        <p class="mb-2"><strong>Sebelum Diurutkan:</strong></p>
        <ul class="flex items-center justify-center gap-2">
          <li v-for="angka in angkaAcak" :key="angka" class="text-lg mb-2">
            {{ angka }}
          </li>
        </ul>
      </div>
      <div>
        <p class="mt-4"><strong>Setelah Diurutkan:</strong></p>
        <ul class="flex items-center justify-center gap-2 mb-2">
          <li
            v-for="mengurutkan in angkaUrut"
            :key="mengurutkan"
            class="text-lg mb-2"
          >
            {{ mengurutkan }}
          </li>
        </ul>
      </div>

      <!-- 9 -->
      <h1 class="text-2xl font-bold my-4">9. Word List Component</h1>
      <div>
        <p><strong>Kata Sebelum Diubah:</strong></p>
        <ul class="flex items-center justify-center space-x-4">
          <li
            v-for="mengacak in angkaAsli"
            :key="mengacak"
            class="text-lg mb-2"
          >
            {{ mengacak }}
          </li>
        </ul>
      </div>
      <div>
        <p class="mt-4"><strong>Kata Sesudah Diubah: menghapus tiga</strong></p>
        <ul class="flex items-center justify-center space-x-4 mb-4">
          <li v-for="urutkan in kosong" :key="urutkan" class="text-lg mb-2">
            {{ urutkan }}
          </li>
        </ul>
      </div>

      <!-- 10 -->
      <h1 class="text-2xl font-bold my-4">10. Square Component</h1>
      <div>
        <p>Sebelum Transformasi:</p>
        <ul class="flex items-center justify-center gap-4">
          <li
            v-for="sebelum in angkaSebelum"
            :key="sebelum"
            class="text-lg mb-2"
          >
            {{ sebelum }}
          </li>
        </ul>
      </div>
      <div>
        <p class="mt-4">Setelah Transformasi:</p>
        <ul class="flex items-center justify-center gap-4 mb-5">
          <li
            v-for="hasilnya in transformasiAngka"
            :key="hasilnya"
            class="text-lg mb-2"
          >
            {{ hasilnya }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
// 1&2
const daftarBelanja = ref([]);
daftarBelanja.value.push("Apel", "Pisang", "Susu");
daftarBelanja.value.unshift("Roti");
daftarBelanja.value.pop();

// 3
const arrayAwal = ref([5, 10, 15, 20, 25]);
const arrayGenap = arrayAwal.value.filter((number) => number % 2 === 0);

// 4
const arrayKata = ref(["apel", "pisang", "jeruk", "mangga"]);
const cariBuah = (kata) => {
  return arrayKata.value.indexOf(kata);
};

// 5
const mencariKataBuah = ref(["apel", "pisang", "jeruk", "mangga", "anggur"]);
const cariKata = ref("");
const hasilDitemukan = ref(-1);

const cari = () => {
  hasilDitemukan.value = mencariKataBuah.value.indexOf(cariKata.value);
};

// 6
const ticTacToe = ref([
  ["X", "O", "X"],
  ["O", "X", "O"],
  ["X", "O", "X"],
]);

// 7
const array1 = ref([1, 2, 3]);
const array2 = ref([4, 5, 6]);
const arrayBaru = ref([]);
onMounted(() => {
  arrayBaru.value = [...array1.value, ...array2.value];
});

//  8
const fungsiAngkaAcak = () => {
  return Array.from({ length: 6 }, () => Math.floor(Math.random() * 10) + 1);
};

const angkaAcak = ref(fungsiAngkaAcak());

const angkaUrut = ref([]);

const fungsiMengurutkanAngka = () => {
  angkaUrut.value = [...angkaAcak.value].sort((a, b) => a - b);
};

onMounted(() => {
  fungsiMengurutkanAngka();
});

// 9
const angkaAsli = ref(["satu", "dua", "tiga", "empat", "lima"]);

const kosong = ref([]);

const hapusKata = (kata) => {
  const index = kosong.value.indexOf(kata);
  if (index !== -1) {
    kosong.value.splice(index, 1);
  }
};

onMounted(() => {
  kosong.value = [...angkaAsli.value];
  const kataYangAkanDihapus = "tiga";
  hapusKata(kataYangAkanDihapus);
});

// 10
const angkaSebelum = ref([2, 4, 6, 8, 10]);

const transformasiAngka = ref([]);

const pangkatDua = (array) => array.map((elemen) => elemen ** 2);

onMounted(() => {
  transformasiAngka.value = pangkatDua(angkaSebelum.value);
});
</script>
