<template>
    <div>
      <h2 class="text-xl mb-4">Education Information</h2>
      <div>
        <input v-model="localData.school" type="text" placeholder="School/College Name" class="w-full mb-4 p-2 border" @input="validate" />
        <span v-if="errors.school" class="text-red-500">{{ errors.school }}</span>
      </div>
      <div>
        <input v-model="localData.graduation" type="text" placeholder="Graduation Year" class="w-full mb-4 p-2 border" @input="validate" />
        <span v-if="errors.graduation" class="text-red-500">{{ errors.graduation }}</span>
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
        const yearRegex = /^(19|20)\d{2}$/;
  
        if (!this.localData.school.trim()) {
          this.errors.school = 'School/College Name is required.';
        }
        if (!yearRegex.test(this.localData.graduation)) {
          this.errors.graduation = 'Graduation Year must be a valid year (1900-2099).';
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
  