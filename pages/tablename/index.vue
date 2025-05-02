<template>
  <div class="relative">
    <div class="absolute left-140 top-50">
      <table cellspacing="0">
        <thead
          class="outline-2 outline-offset-2 outline-solid rounded-xl bg-blue-500"
        >
          <tr>
            <th class="w-96">ชื่อ</th>
            <th class="w-96">นามสกุล</th>
          </tr>
        </thead>
        <tbody>
          <tr class="text-center" v-for="(item, index) in FName" :key="index">
            <td class="border border-gray-300">{{ item.name }}</td>
            <td class="border border-gray-300">{{ item.surname }}</td>
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
  },
  {
    name: "B",
    surname: "BB",
  },
];

FName.value = Fullname;

console.log(FName);

//ทำ ชื่อ นามสกุล อายุ ที่อยู่
</script>
