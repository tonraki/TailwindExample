<template>
    <div class="container mx-auto p-6 bg-black-200 shadow-lg rounded-lg max-w-100 mt-50">
        <h1 class="text-2xl mb-7 text-center font-bold font-serif">เข้าสู่ระบบ</h1>

        <div>
          <label class="block text-gray-700">อีเมล</label>
          <input 
            type="email" 
            v-model="email"
            placeholder="กรอกอีเมลของคุณ" 
            class="w-full mt-2 p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-400" 
            
          />
        </div>
        <div class="mt-4">
          <label class="block text-gray-700">รหัสผ่าน</label>
          <input 
            type="password" 
            v-model="password"
            placeholder="กรอกรหัสผ่าน" 
            class="w-full mt-2 p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-400" 
            
          />
        </div>

<div>
    <button @click="formLogin" class="w-full mt-6 bg-green-500 hover:bg-blue-600 text-white font-semibold py-3 rounded-lg transition duration-300">ล็อคอินเข้าสู่ระบบ</button>
</div>

<div class="text-center mt-4 text-gray-700">
  <span>ยังไม่มีบัญชีใช่ไหม?</span>
  <a href="/register" class="text-blue-500 hover:underline ml-1">ลงทะเบียนสิ</a>
</div>

<footer class="border-gray-300 py-6 text-center text-white">
      <img src="/assets/css/images/banner-jeed777.webp" alt="Footer Image" class="p-1 max-w-90 h-32 mx-auto mb-3 mt-1">
      <p>© 2025 My Website | All Rights Reserved</p>
    </footer>


    </div>
</template>

<script setup>

const formLogin = () => {
    console.log(formLogin);
    
};

</script>