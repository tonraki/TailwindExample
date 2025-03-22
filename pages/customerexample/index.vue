<template>
    <div class="max-w-3xl mx-auto p-6 bg-white shadow-lg rounded-lg">
      <h2 class="text-2xl font-bold text-gray-800 mb-4">Add User</h2>
  
      <!-- Input Fields -->
      <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
        <input
          v-model="formData.name"
          type="text"
          placeholder="Enter Name"
          class="w-full border rounded-lg px-4 py-2 focus:ring focus:ring-blue-300"
        />
        <input
          v-model="formData.email"
          type="email"
          placeholder="Enter Email"
          class="w-full border rounded-lg px-4 py-2 focus:ring focus:ring-blue-300"
        />
        <input
          v-model="formData.age"
          type="number"
          placeholder="Enter Age"
          class="w-full border rounded-lg px-4 py-2 focus:ring focus:ring-blue-300"
        />
      </div>
  
      <!-- Submit Button -->
      <button
        @click="addToTable"
        class="mt-4 w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 rounded-lg transition"
      >
        Add to Table
      </button>
  
      <!-- Data Table -->
      <div v-if="tableData.length" class="mt-6">
        <h3 class="text-xl font-semibold text-gray-700 mb-3">User List</h3>
  
        <div class="overflow-x-auto">
          <table class="w-full bg-white shadow-md rounded-lg overflow-hidden">
            <thead class="bg-gray-100">
              <tr>
                <th class="px-4 py-2 text-left text-gray-700">Name</th>
                <th class="px-4 py-2 text-left text-gray-700">Email</th>
                <th class="px-4 py-2 text-left text-gray-700">Age</th>
                <th class="px-4 py-2 text-left text-gray-700">Actions</th>
              </tr>
            </thead>
            <tbody>
              <tr
                v-for="(item, index) in tableData"
                :key="index"
                class="border-t hover:bg-gray-50 transition"
              >
                <td class="px-4 py-2">{{ item.name }}</td>
                <td class="px-4 py-2">{{ item.email }}</td>
                <td class="px-4 py-2">{{ item.age }}</td>
                <td class="px-4 py-2">
                  <button
                    @click="removeItem(index)"
                    class="bg-blue-500 hover:bg-red-600 text-red px-3 py-1 rounded-lg transition"
                  >
                    Delete
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  // Reactive state for form input and table data
  const formData = ref({
    name: '',
    email: '',
    age: ''
  })  

//   console.log(formData);
  
  const tableData = ref([])
  
//   console.log(tableData);
  
  // Function to add input data to the table
  const addToTable = () => { 
  
    if (formData.value.name && formData.value.email && formData.value.age) {
      tableData.value.push({ ...formData.value })

    //   console.log(formData.value.email);
    //   console.log(formData.value.name);
      
      
      
  
      // Clear input fields after adding
      formData.value.name = ''
      formData.value.email = ''
      formData.value.age = ''

    //   console.log(formData.value.name);
      
    } else {
      alert('Please fill in all fields!')      
    }
  }
  
  // Function to remove a row from the table
  const removeItem = (index) => {
    tableData.value.splice(index, 1)
    // console.log(removeItem);
    
  }
  </script>