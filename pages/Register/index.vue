<template>
    <div class="container mx-auto p-6 bg-black-200 shadow-lg rounded-lg max-w-100 mt-50">
        <h1 class="text-center text-xl font-bold mb-5">ลงทะเบียน</h1>

        <div>
          <label class="block text-gray-700 mt-2">อีเมล</label>
          <input 
            type="email" 
            v-model="email"
            placeholder="กรุณากรอกอีเมลของคุณ" 
            class="w-full mt-2 p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-400" 
            
          />
        </div>
        <div>
          <label class="block text-gray-700 mb-1 mt-2">รหัสผ่าน</label>
          <input 
            type="password" 
            v-model="password"
            placeholder="กรุณาตั้งรหัสผ่าน" 
            class="w-full mt-2 p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-400" 
            
          />
        </div>
        <div>
            <button @click="formRegister" class="w-full mt-6 bg-green-500 hover:bg-blue-600 text-white font-semibold py-3 rounded-lg transition duration-300">ลงทะเบียนตอนนี้</button>
        </div>

    </div>

</template>

<script setup>

const formRegister = () => {
    console.log(formRegister);
    
}
</script>