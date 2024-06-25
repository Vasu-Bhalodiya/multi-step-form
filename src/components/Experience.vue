<template>
    <div>
      <h2 class="text-xl mb-4">Experience Information</h2>
      <div>
        <input v-model="localData.company" type="text" placeholder="Company Name" class="w-full mb-4 p-2 border" @input="validate" />
        <span v-if="errors.company" class="text-red-500">{{ errors.company }}</span>
      </div>
      <div>
        <input v-model="localData.role" type="text" placeholder="Role in Company" class="w-full mb-4 p-2 border" @input="validate" />
        <span v-if="errors.role" class="text-red-500">{{ errors.role }}</span>
      </div>
    </div>
  </template>
  
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
  
        if (!this.localData.company.trim()) {
          this.errors.company = 'Company Name is required.';
        }
        if (!this.localData.role.trim()) {
          this.errors.role = 'Role in Company is required.';
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
  