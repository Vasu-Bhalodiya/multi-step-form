<template>
    <div>
      <h2 class="text-xl mb-4">Personal Information</h2>
      <div>
        <input v-model="localData.firstName" type="text" placeholder="First Name" class="w-full mb-4 p-2 border" @input="validate" />
        <span v-if="errors.firstName" class="text-red-500">{{ errors.firstName }}</span>
      </div>
      <div>
        <input v-model="localData.lastName" type="text" placeholder="Last Name" class="w-full mb-4 p-2 border" @input="validate" />
        <span v-if="errors.lastName" class="text-red-500">{{ errors.lastName }}</span>
      </div>
      <div>
        <input v-model="localData.email" type="email" placeholder="Email" class="w-full mb-4 p-2 border" @input="validate" />
        <span v-if="errors.email" class="text-red-500">{{ errors.email }}</span>
      </div>
      <div>
        <input v-model="localData.mobileNumber" type="tel" placeholder="Mobile Number" class="w-full mb-4 p-2 border" @input="validate" />
        <span v-if="errors.mobileNumber" class="text-red-500">{{ errors.mobileNumber }}</span>
      </div>
    </div>
  </template>
  <!-- TEST -->
  <script>
  export default {
    props: {
      data: Object
    },
    data() {
      return {
        localData: { ...this.data },
        errors: {}
      };
    },
    methods: {
      validate() {
        this.errors = {};
        const nameRegex = /^[A-Za-z]+$/;
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        const phoneRegex = /^[0-9]{10}$/;
  
        if (!nameRegex.test(this.localData.firstName)) {
          this.errors.firstName = 'First Name must contain only letters.';
        }
        if (!nameRegex.test(this.localData.lastName)) {
          this.errors.lastName = 'Last Name must contain only letters.';
        }
        if (!emailRegex.test(this.localData.email)) {
          this.errors.email = 'Invalid email format.';
        }
        if (!phoneRegex.test(this.localData.mobileNumber)) {
          this.errors.mobileNumber = 'Mobile Number must be 10 digits.';
        }
  
        return Object.keys(this.errors).length === 0;
      }
    },
    watch: {
      localData: {
        handler() {
          this.$emit('update', { ...this.localData });
        },
        deep: true
      }
    }
  };
  </script>
  
  <style scoped>
  </style>
  