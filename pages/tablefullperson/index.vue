<template>

  <div class="flex justify-center items-center min-h-screen bg-gray-50">
    <div class="overflow-hidden shadow-lg rounded-lg">
        
      <table class="table-auto border-collapse border border-gray-300 bg-white">

        <thead class="bg-gray-200 text-gray-700">
          <tr>
            <th class="border border-gray-300 px-6 py-3 text-left">ชื่อ</th>
            <th class="border border-gray-300 px-6 py-3 text-left">นามสกุล</th>
            <th class="border border-gray-300 px-6 py-3 text-left">อายุ</th>
            <th class="border border-gray-300 px-6 py-3 text-left">ที่อยู่</th>
          </tr>
        </thead>

        <tbody>
          <tr class="hover:bg-gray-100" v-for="(item, index) in FName" :key="index">
            <td class="border border-gray-300 px-6 py-3">{{ item.name }}</td>
            <td class="border border-gray-300 px-6 py-3">{{ item.surname }}</td>
            <td class="border border-gray-300 px-6 py-3">{{ item.old }}</td>
            <td class="border border-gray-300 px-6 py-3">{{ item.address }}</td>
          </tr>
        </tbody>

      </table>
    </div>
  </div>

</template>

<script setup>
import { ref } from "vue";

const FName = ref();
let Fullname = [
  {
    name: "A",
    surname: "AA",
    old: 15,
    address: 'BKK'
  },
  {
    name: "B",
    surname: "BB",
    old: 16,
    address: 'SNO'
  },{
    name: "C",
    surname: "CC",
    old: 16,
    address: 'CNX'
  },{
    name: "D",
    surname: "DD",
    old: 16,
    address: 'HKT'
  }]

FName.value = Fullname;
console.log(FName);

</script>
