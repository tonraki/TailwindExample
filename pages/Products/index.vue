<template>
    <div class="min-h-screen bg-gradient-to-br from-green-100 via-white to-green-200 py-12 px-6">
      <div class="flex flex-col items-center">
        <h1 class="text-4xl font-bold text-center text-green-700 mb-10 drop-shadow">รายการสินค้า</h1>
        
        <!-- ปุ่มตะกร้าสินค้า -->
        <div class="self-end mb-6">
          <button 
            @click="showCart" 
            class="flex items-center gap-2 px-4 py-2 bg-green-600 rounded-full hover:bg-green-700 shadow-md transition"
          >
            <span class="text-xl">🛒</span>
            <span>ตะกร้าสินค้า</span>
            <span v-if="cartItems.length > 0" class="bg-white text-green-700 rounded-full w-6 h-6 flex items-center justify-center text-sm font-bold">
              {{ cartItems.length }}
            </span>
          </button>
        </div>
        
        <!-- รายการสินค้า -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 w-full max-w-6xl">
          <div
            v-for="(product, index) in products"
            :key="index"
            class="bg-white rounded-lg shadow-md p-6 flex flex-col"
          >
            <h2 class="text-xl font-semibold text-gray-800 mb-2">{{ product.name }}</h2>
            <p class="text-gray-500 text-sm mb-4">{{ product.description }}</p>
            <p class="text-green-600 text-lg font-bold mb-4">{{ product.price }} บาท</p>
            
            <div class="flex items-center mt-auto">
              <div class="flex items-center border rounded-lg overflow-hidden mr-2">
                <button 
                  @click="decreaseQuantity(product)" 
                  class="px-3 py-1 bg-gray-100 hover:bg-gray-200"
                  :disabled="!getCartQuantity(product)"
                >-</button>
                <span class="px-4 py-1">{{ getCartQuantity(product) }}</span>
                <button 
                  @click="increaseQuantity(product)" 
                  class="px-3 py-1 bg-gray-100 hover:bg-gray-200"
                >+</button>
              </div>
              
              <button
                @click="addToCart(product)"
                class="flex-1 px-4 py-2 bg-green-500 text-white rounded-full hover:bg-green-600 shadow-md transition"
              >
                เพิ่มลงตะกร้า
              </button>
            </div>
          </div>
        </div>
        
        <!-- ตารางสินค้า -->
        <div class="w-full max-w-6xl mt-12" v-if="purchasedItems.length > 0">
          <h2 class="text-2xl font-bold text-center text-green-700 mb-6">ประวัติการสั่งซื้อ</h2>
          <table class="w-full bg-white rounded-lg overflow-hidden shadow-md">
            <thead class="bg-green-100">
              <tr>
                <th class="border border-gray-300 px-6 py-3 text-left">รายการสินค้า</th>
                <th class="border border-gray-300 px-6 py-3 text-left">รายละเอียด</th>
                <th class="border border-gray-300 px-6 py-3 text-left">จำนวน</th>
                <th class="border border-gray-300 px-6 py-3 text-left">ราคาต่อชิ้น</th>
                <th class="border border-gray-300 px-6 py-3 text-left">รวม</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(item, index) in purchasedItems" :key="index">
                <td class="border border-gray-300 px-6 py-4">{{ item.name }}</td>
                <td class="border border-gray-300 px-6 py-4">{{ item.description }}</td>
                <td class="border border-gray-300 px-6 py-4 text-center">{{ item.quantity }}</td>
                <td class="border border-gray-300 px-6 py-4 text-right">{{ item.price }} บาท</td>
                <td class="border border-gray-300 px-6 py-4 text-right">{{ item.price * item.quantity }} บาท</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      
      <!-- Modal ตะกร้าสินค้า -->
      <div
        v-if="showCartModal"
        class="fixed inset-0 bg-black bg-opacity-40 flex items-center justify-center z-50"
      >
        <div class="bg-white rounded-2xl p-6 max-w-2xl w-full shadow-lg relative max-h-[90vh] overflow-y-auto">
          <button
            @click="showCartModal = false"
            class="absolute top-4 right-4 text-gray-500 text-2xl hover:text-red-500"
          >
            &times;
          </button>
  
          <h2 class="text-2xl font-semibold text-center text-green-700 mb-6">ตะกร้าสินค้าของคุณ</h2>
          
          <div v-if="cartItems.length === 0" class="text-center text-gray-500 py-8">
            ตะกร้าสินค้าว่างเปล่า
          </div>
          
          <div v-else>
            <div class="space-y-4 mb-6">
              <div v-for="(item, index) in cartItems" :key="index" class="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                <div class="flex-1">
                  <h3 class="font-medium">{{ item.name }}</h3>
                  <p class="text-sm text-gray-500">{{ item.price }} บาท</p>
                </div>
                
                <div class="flex items-center">
                  <div class="flex items-center border rounded-lg overflow-hidden mr-2">
                    <button 
                      @click="decreaseQuantity(item)" 
                      class="px-2 py-1 bg-gray-100 hover:bg-gray-200"
                    >-</button>
                    <span class="px-3 py-1">{{ item.quantity }}</span>
                    <button 
                      @click="increaseQuantity(item)" 
                      class="px-2 py-1 bg-gray-100 hover:bg-gray-200"
                    >+</button>
                  </div>
                  
                  <button 
                    @click="removeFromCart(item)" 
                    class="text-red-500 hover:text-red-700 ml-2"
                  >
                    🗑️
                  </button>
                </div>
              </div>
            </div>
            
            <div class="border-t border-gray-200 pt-4 mb-6">
              <div class="flex justify-between items-center font-medium">
                <span>รวมทั้งสิ้น:</span>
                <span class="text-xl font-bold text-green-600">{{ calculateTotal() }} บาท</span>
              </div>
            </div>
            
            <div class="flex justify-center gap-4">
              <button
                @click="clearCart"
                class="bg-gray-300 text-gray-800 px-4 py-2 rounded-full hover:bg-gray-400 transition"
              >
                ล้างตะกร้า
              </button>
              <button
                @click="confirmCheckout"
                class="bg-green-500 text-white px-6 py-2 rounded-full hover:bg-green-600 transition"
              >
                ยืนยันการสั่งซื้อ
              </button>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Modal ยืนยันการสั่งซื้อ -->
      <div
        v-if="showConfirmModal"
        class="fixed inset-0 bg-black bg-opacity-40 flex items-center justify-center z-50"
      >
        <div class="bg-white rounded-2xl p-6 max-w-md w-full shadow-lg relative">
          <button
            @click="showConfirmModal = false"
            class="absolute top-2 right-3 text-gray-500 text-2xl hover:text-red-500"
          >
            &times;
          </button>
  
          <h2 class="text-xl font-semibold text-center text-green-700 mb-4">ยืนยันการสั่งซื้อ</h2>
          <p class="text-center text-gray-600 mb-6">
            คุณต้องการยืนยันการสั่งซื้อสินค้าจำนวน {{ cartItems.length }} รายการ
            รวมเป็นเงินทั้งสิ้น <strong>{{ calculateTotal() }}</strong> บาท ใช่หรือไม่?
          </p>
  
          <div class="flex justify-center gap-4">
            <button
              @click="completeOrder"
              class="bg-green-500 text-white px-4 py-2 rounded-full hover:bg-green-600 transition"
            >
              ยืนยัน
            </button>
            <button
              @click="showConfirmModal = false"
              class="bg-gray-300 text-gray-800 px-4 py-2 rounded-full hover:bg-gray-400 transition"
            >
              ยกเลิก
            </button>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from "vue";
  
  const showCartModal = ref(false);
  const showConfirmModal = ref(false);
  const cartItems = ref([]);
  const purchasedItems = ref([]);
  
  const products = [
    {
      name: 'เสื้อยืดสุดเท่',
      description: 'ใส่แล้วเท่จนคนเหลียวมอง',
      price: 250
    },
    {
      name: 'หมวกแฟชั่น',
      description: 'หมวกสวย ใส่แล้วดูดี',
      price: 150
    },
    {
      name: 'กระเป๋าเป้',
      description: 'เหมาะสำหรับนักเดินทาง',
      price: 450
    },
    {
      name: 'รองเท้าสปอร์ต',
      description: 'เบา ใส่สบาย สำหรับออกกำลังกาย',
      price: 990
    },
    {
      name: 'แว่นกันแดด',
      description: 'เท่และป้องกันแสงแดดได้ดี',
      price: 299
    },
    {
      name: 'นาฬิกาข้อมือ',
      description: 'ดูเวลาอย่างมีสไตล์',
      price: 799
    }
  ];
  
  const showCart = () => {
    showCartModal.value = true;
  };
  
  const addToCart = (product) => {
    const existingItem = cartItems.value.find(item => item.name === product.name);
    
    if (existingItem) {
      existingItem.quantity += 1;
    } else {
      cartItems.value.push({ ...product, quantity: 1 });
    }
  };
  
  const getCartQuantity = (product) => {
    const existingItem = cartItems.value.find(item => item.name === product.name);
    return existingItem ? existingItem.quantity : 0;
  };
  
  const increaseQuantity = (product) => {
    const existingItem = cartItems.value.find(item => item.name === product.name);
    
    if (existingItem) {
      existingItem.quantity += 1;
    } else {
      addToCart(product);
    }
  };
  
  const decreaseQuantity = (product) => {
    const existingItem = cartItems.value.find(item => item.name === product.name);
    
    if (existingItem && existingItem.quantity > 1) {
      existingItem.quantity -= 1;
    } else if (existingItem && existingItem.quantity === 1) {
      removeFromCart(product);
    }
  };
  
  const removeFromCart = (product) => {
    cartItems.value = cartItems.value.filter(item => item.name !== product.name);
  };
  
  const calculateTotal = () => {
    return cartItems.value.reduce((total, item) => total + (item.price * item.quantity), 0);
  };
  
  const clearCart = () => {
    cartItems.value = [];
  };
  
  const confirmCheckout = () => {
    if (cartItems.value.length > 0) {
      showCartModal.value = false;
      showConfirmModal.value = true;
    }
  };
  
  const completeOrder = () => {
    // เพิ่มรายการที่ซื้อไปยังประวัติการสั่งซื้อ
    cartItems.value.forEach(item => {
      purchasedItems.value.push({ ...item });
    });
    
    // ล้างตะกร้า
    clearCart();
    showConfirmModal.value = false;
  };
  </script>