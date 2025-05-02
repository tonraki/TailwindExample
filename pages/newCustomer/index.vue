<template>

  <div class="container mx-auto p-6 bg-blue-100 shadow-lg rounded-lg max-w-4xl mt-20">
    <h1 class="text-2xl font-semibold mb-6 text-center text-black-300">ข้อมูลลูกค้า</h1>
    <div class="mb-2">
        <label> ชื่อ : </label>
    <input type="text" v-model="fromdataUser.name" placeholder="กรุณากรอกชื่อ" class="w-full p-3 mt-1 border border-gray-300 rounded-md focus:ring-2 focus:ring-blue-500 focus:outline-none" />
    </div>
    
    <div class="mb-2">
        <label> นามสกุล : </label>
    <input type="text" v-model="fromdataUser.surname" placeholder="กรุณากรอกนามสกุล" class="w-full p-3 mt-1 border border-gray-300 rounded-md focus:ring-2 focus:ring-blue-500 focus:outline-none" />
    </div>
    <div class="mb-2">
        <label> อายุ : </label>
        <input type="text" v-model="fromdataUser.old" placeholder="กรุณากรอกอายุ" class="w-full p-3 mt-1 border border-gray-300 rounded-md focus:ring-2 focus:ring-blue-500 focus:outline-none" />
    </div>
    
    <div class="mb-2">
        <label> ที่อยู่ : </label>
    <input type="text" v-model="fromdataUser.address" placeholder="กรุณากรอกที่อยู่" class="w-full p-3 mt-1 border border-gray-300 rounded-md focus:ring-2 focus:ring-blue-500 focus:outline-none" />
    </div>
    
    <div class="mb-2">
        <select v-model="fromdataUser.provice" class="w-full p-3 mt-1 border border-gray-300 rounded-md focus:ring-2 focus:ring-blue-500 focus:outline-none">
      <option value="" disabled>เลือกจังหวัดของคุณ</option>
      <option v-for="(province, index) in dataProvice" :key="index" :value="province" >
        {{ province }}
      </option>
    </select>
    </div>
    


    <!-- <p>{{ fromdataUser }}</p> -->

    <div class="text-center">
      <button @click="addToTable" 
        class="w-full py-3 bg-yellow-500 text-white font-semibold rounded-lg shadow-md hover:bg-green-600 focus:outline-none focus:ring-2 focus:ring-blue-500">
        เพิ่มข้อมูลลูกค้า
      </button>
    </div>

    <div class="mt-7">
        <table class="min-w-full border-collapse bg-white shadow-md rounded-lg">
  <thead class="bg-gray-200">
    <tr>
      <th class="border border-gray-300 px-4 py-2 text-center text-sm text-gray-700">ชื่อ</th>
      <th class="border border-gray-300 px-4 py-2 text-center text-sm text-gray-700">นามสกุล</th>
      <th class="border border-gray-300 px-4 py-2 text-center text-sm text-gray-700">อายุ</th>
      <th class="border border-gray-300 px-4 py-2 text-center text-sm text-gray-700">ที่อยู่</th>
      <th class="border border-gray-300 px-4 py-2 text-center text-sm text-gray-700">จังหวัด</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(item, index) in dataCustomer" :key="index" class="text-center">
        <td class="border border-gray-300 px-4 py-2">{{ item.name }}</td>
        <td class="border border-gray-300 px-4 py-2">{{ item.surname }}</td>
        <td class="border border-gray-300 px-4 py-2">{{ item.old }}</td>
        <td class="border border-gray-300 px-4 py-2">{{ item.address }}</td>
        <td class="border border-gray-300 px-4 py-2">{{ item.provice }}</td>
      
    </tr>

    
    
  </tbody>
</table>
</div>
    
  </div>



</template>

<script setup>

import { ref } from "vue";

const dataProvice = ref(["กรุงเทพมหานคร", "กระบี่", "กาญจนบุรี", "กาฬสินธุ์", "กำแพงเพชร", "ขอนแก่น", "จันทบุรี", "ฉะเชิงเทรา", "ชลบุรี", "ชัยนาท", "ชัยภูมิ", "ชุมพร", "เชียงราย", "เชียงใหม่", "ตรัง", "ตราด", "ตาก", "นครนายก", "นครปฐม", "นครพนม", "นครราชสีมา", "นครศรีธรรมราช", "นครสวรรค์", "นนทบุรี", "นราธิวาส", "น่าน", "บึงกาฬ", "บุรีรัมย์", "ปทุมธานี", "ประจวบคีรีขันธ์", "ปราจีนบุรี", "ปัตตานี", "พระนครศรีอยุธยา", "พังงา", "พัทลุง", "พิจิตร", "พิษณุโลก", "เพชรบุรี", "เพชรบูรณ์", "แพร่", "พะเยา", "ภูเก็ต", "มหาสารคาม", "มุกดาหาร", "แม่ฮ่องสอน", "ยโสธร", "ยะลา", "ร้อยเอ็ด", "ระนอง", "ระยอง", "ราชบุรี", "ลพบุรี", "ลำปาง", "ลำพูน", "เลย", "ศรีสะเกษ", "สกลนคร", "สงขลา", "สตูล", "สมุทรปราการ", "สมุทรสงคราม", "สมุทรสาคร", "สระแก้ว", "สระบุรี", "สิงห์บุรี", "สุโขทัย", "สุพรรณบุรี", "สุราษฎร์ธานี", "สุรินทร์", "หนองคาย", "หนองบัวลำภู", "อ่างทอง", "อำนาจเจริญ", "อุดรธานี", "อุตรดิตถ์", "อุทัยธานี", "อุบลราชธานี"])

const fromdataUser = ref({
    name: '',
    surname: '',
    old: '',
    address: '',
    provice: ''
});
// console.log(fromdata);

const dataCustomer = ref([])

const addToTable = () =>{
    // console.log(addToTable);
    dataCustomer.value.push({...fromdataUser.value})
}


</script>
