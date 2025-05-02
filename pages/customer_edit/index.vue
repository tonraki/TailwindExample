<template>
<div class="flex flex-col items-center bg-pink-100 min-h-screen p-6">
    <div class="bg-white shadow-lg rounded-lg p-6 w-full max-w-md">
        <h1 class="text-2xl font-bold text-center text-blue-600 mb-4">ตารางสินค้า</h1>

        <div class="space-y-3">
            <input
          v-model="dataProduct.name"
          class="w-full bg-gray-50 placeholder:text-gray-400 text-gray-700 text-sm border border-gray-300 rounded-md px-4 py-2 focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-300"
          placeholder="ชื่อสินค้า"
        />

        <input
          v-model="dataProduct.qty"
          type="number"
          class="w-full bg-gray-50 placeholder:text-gray-400 text-gray-700 text-sm border border-gray-300 rounded-md px-4 py-2 focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-300"
          placeholder="จำนวน"
        />

        <input
          v-model="dataProduct.price"
          type="number"
          class="w-full bg-gray-50 placeholder:text-gray-400 text-gray-700 text-sm border border-gray-300 rounded-md px-4 py-2 focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-300"
          placeholder="ราคา"
        />

        <select
          v-model="dataProduct.province"
          class="w-full bg-gray-50 text-gray-700 text-sm border border-gray-300 rounded-md px-4 py-2 focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-300"
        >
          <option value="" disabled selected>เลือกจังหวัด</option>
          <option v-for="province in provinces" :key="province" :value="province">
            {{ province }}
          </option>
        </select>

        <button
          @click="addToTable"
          class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 rounded-md transition duration-300 shadow-md"
        >
          เพิ่มสินค้า
        </button>
        </div>
    </div>

    <div class="w-full max-w-2xl mt-6">
      <table class="w-full bg-white shadow-lg rounded-lg overflow-hidden">
        <thead>
          <tr class="bg-blue-600 text-white">
            <th class="px-6 py-3 text-center">ชื่อ</th>
            <th class="px-6 py-3 text-center">จำนวน (ชิ้น)</th>
            <th class="px-6 py-3 text-center">ราคา (บาท)</th>
            <th class="px-6 py-3 text-center">จังหวัด</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(item, index) in customer"
            :key="index"
            class="border-b border-gray-300 hover:bg-gray-100 text-center"
          >
            <td class="px-6 py-3">{{ item.name }}</td>
            <td class="px-6 py-3">{{ item.qty }}</td>
            <td class="px-6 py-3">{{ item.price }}.-</td>
            <td class="px-6 py-3">{{ item.province }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const provinces = [
  "กรุงเทพมหานคร", "กระบี่", "กาญจนบุรี", "กาฬสินธุ์", "กำแพงเพชร", "ขอนแก่น", "จันทบุรี", "ฉะเชิงเทรา", "ชลบุรี", "ชัยนาท", "ชัยภูมิ", "ชุมพร", "เชียงราย", "เชียงใหม่", "ตรัง", "ตราด", "ตาก", "นครนายก", "นครปฐม", "นครพนม", "นครราชสีมา", "นครศรีธรรมราช", "นครสวรรค์", "นนทบุรี", "นราธิวาส", "น่าน", "บึงกาฬ", "บุรีรัมย์", "ปทุมธานี", "ประจวบคีรีขันธ์", "ปราจีนบุรี", "ปัตตานี", "พระนครศรีอยุธยา", "พังงา", "พัทลุง", "พิจิตร", "พิษณุโลก", "เพชรบุรี", "เพชรบูรณ์", "แพร่", "พะเยา", "ภูเก็ต", "มหาสารคาม", "มุกดาหาร", "แม่ฮ่องสอน", "ยโสธร", "ยะลา", "ร้อยเอ็ด", "ระนอง", "ระยอง", "ราชบุรี", "ลพบุรี", "ลำปาง", "ลำพูน", "เลย", "ศรีสะเกษ", "สกลนคร", "สงขลา", "สตูล", "สมุทรปราการ", "สมุทรสงคราม", "สมุทรสาคร", "สระแก้ว", "สระบุรี", "สิงห์บุรี", "สุโขทัย", "สุพรรณบุรี", "สุราษฎร์ธานี", "สุรินทร์", "หนองคาย", "หนองบัวลำภู", "อ่างทอง", "อำนาจเจริญ", "อุดรธานี", "อุตรดิตถ์", "อุทัยธานี", "อุบลราชธานี"
];

const dataProduct = ref({
  name: "",
  qty: "",
  price: "",
  provinces:""
});

const customer = ref([]);
const addToTable = () => {

customer.value.push({ ...dataProduct.value });

};
</script>