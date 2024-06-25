<template>
    <div>
      <h2 class="text-xl mb-4">Profile Image</h2>
      <div>
        <input type="file" @change="handleFileUpload" class="w-full mb-4 p-2 border" />
        <span v-if="errors.profileImage" class="text-red-500">{{ errors.profileImage }}</span>
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
        errors: {}
      };
    },
    methods: {
      handleFileUpload(event) {
        const file = event.target.files[0];
        this.errors = {};
  
        if (file && !file.type.match('image.*')) {
          this.errors.profileImage = 'Only image files are allowed.';
        } else {
          this.$emit('update', { profileImage: file });
        }
      },
      validate() {
        if (!this.data.profileImage) {
          this.errors.profileImage = 'Profile image is required.';
          return false;
        }
        return true;
      }
    }
  };
  </script>
  
  <style scoped>
  </style>
  