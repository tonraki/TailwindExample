<template>

<h1 class="ml-200">ตารางสินค้า</h1>
<div class="flex justify-center items-center min-h-screen bg-gray-50">
    <table class="border-collapse border border-gray-400 rounded">
  <thead>
    <tr>
      <th class="border border-gray-300 ">ชื่อ</th>
      <th class="border border-gray-300 ">จำนวน(ชิ้น)</th>
      <th class="border border-gray-300 ">ราคา(บาท)</th>
      
    </tr>
  </thead>
  <tbody>
          <tr class="hover:bg-gray-100" v-for="(item, index) in customer" :key="index">
            <td class="border border-gray-300 px-6 py-3">{{ item.name }}</td>
            <td class="border border-gray-300 px-6 py-3">{{ item.qty }}</td>
            <td class="border border-gray-300 px-6 py-3">{{ item.price }}</td>
        <div class="flex justify-center mb-4 mt-5">
      <button 
        @click="addProduct"
        class="bg-green-500 hover:bg-green-700 text-white font-bold py-1 px-0.5 rounded">
        เพิ่มสินค้า
      </button>
    </div>
          </tr>

        </tbody>
</table>
</div>


</template>

<script setup>
import { ref } from "vue";

const customer = ref();
const data = [
  {
    name: "แปรงสิฟัน",
    qty: 100,
    price: 15
  },
  {
    name: "รองเท้า",
    qty: 150,
    price: 299
  },{
    name: "ลูกอม",
    qty: 500,
    price: 10
  }]

customer.value = data;
console.log(customer);

</script>