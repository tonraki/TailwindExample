<template>
  <div class="flex flex-col items-center bg-gray-50">
    
      <h1 class="text-center mt-10 mb-5">ตารางสินค้า</h1>
    

    <div class="w-full max-w-sm space-y-2">
      <input
        v-model="dataProduct.name"
        class="w-full bg-transparent placeholder:text-slate-400 text-slate-700 text-sm border border-slate-200 rounded-md px-3 py-2 transition duration-300 ease focus:outline-none focus:border-slate-400 hover:border-slate-300 shadow-sm focus:shadow"
        placeholder="ชื่อสินค้า"
      />

      <input
        v-model="dataProduct.qty"
        class="w-full bg-transparent placeholder:text-slate-400 text-slate-700 text-sm border border-slate-200 rounded-md px-3 py-2 transition duration-300 ease focus:outline-none focus:border-slate-400 hover:border-slate-300 shadow-sm focus:shadow"
        placeholder="จำนวน"
      />

      <input
        v-model="dataProduct.price"
        class="w-full bg-transparent placeholder:text-slate-400 text-slate-700 text-sm border border-slate-200 rounded-md px-3 py-2 transition duration-300 ease focus:outline-none focus:border-slate-400 hover:border-slate-300 shadow-sm focus:shadow"
        placeholder="ราคา"
      />

      <button
        @click="addToTable"
        class="mt-4 w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 rounded-lg transition"
      >
        เพิ่มสินค้า
      </button>
    </div>
<div class="w-full flex justify-center">
  <table
      class="w-full max-w-lg mt-10 mb-10"
    >
      <thead>
        <tr class="text-blue-600 dark:text-sky-400">
          <th class="border border-gray-300 px-4 py-2 text-center">ชื่อ</th>
          <th class="border border-gray-300 px-4 py-2 text-center">
            จำนวน(ชิ้น)
          </th>
          <th class="border border-gray-300 px-4 py-2 text-center">
            ราคา(บาท)
          </th>
        </tr>
      </thead>

      <tbody>
          <tr
            class="hover:bg-gray-100 text-center"
            v-for="(item, index) in customer"
            :key="index"
          >
            <td class="border border-gray-300 px-6 py-3">{{ item.name }}</td>
            <td class="border border-gray-300 px-6 py-3">{{ item.qty }}</td>
            <td class="border border-gray-300 px-6 py-3">{{ item.price }}</td>
          </tr>
        
      </tbody>
    
    </table>
</div>
    
  </div>
</template>

<script setup>
import { ref } from "vue";

const dataProduct = ref({
  name: "",
  qty: "",
  price: "",
});

const customer = ref([]);
const addToTable = () => {
  console.log(dataProduct.value.name);
  console.log(dataProduct.value.qty);
  console.log(dataProduct.value.price);

  customer.value.push({ ...dataProduct.value });

  //จัดหน้าใช้ grid layout
};
</script>
