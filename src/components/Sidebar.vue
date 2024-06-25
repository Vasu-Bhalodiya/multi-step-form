<template>
    <div class="w-1/4 bg-white shadow-lg">
      <div class="p-6">
        <h2 class="text-xl font-bold mb-6">Step {{ currentStep }}</h2>
        <ul>
          <li v-for="(step, index) in steps" :key="index" @click="changeStep(index + 1)" class="cursor-pointer py-2 px-4 flex items-center" :class="{'bg-blue-100': currentStep === index + 1}">
            <span class="mr-3">{{ index + 1 }}</span>
            <span>{{ stepTitles[index] }}</span>
          </li>
        </ul>
      </div>
    </div>
  </template>
  
  <script>
import UserDetails from './UserDetails.vue';

  export default {
    props: {
      currentStep: Number
    },
    data() {
      return {
        steps: [1, 2, 3, 4,5],
        stepTitles: ['Personal Information', 'Education', 'Work Experiences', 'User Photo','User Details']
      };
    },
    methods: {
      changeStep(step) {
        this.$emit('changeStep', step);
      }
    }
  };
  </script>
  
  <style scoped>
  </style>
  