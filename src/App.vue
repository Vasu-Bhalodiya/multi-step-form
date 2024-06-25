<template>
  <div class="flex h-screen">
    <Sidebar :currentStep="currentStep" @changeStep="goToStep" />
    <div class="flex-grow p-10 bg-gray-100">
      <div v-if="currentStep === 1">
        <PersonalInformation ref="step1" :data="formData" @update="updateFormData" />
      </div>
      <div v-if="currentStep === 2">
        <Education ref="step2" :data="formData" @update="updateFormData" />
      </div>
      <div v-if="currentStep === 3">
        <Experience ref="step3" :data="formData" @update="updateFormData" />
      </div>
      <div v-if="currentStep === 4">
        <ProfileImage ref="step4" :data="formData" @update="updateFormData" />
      </div>
      <div v-if="currentStep === 5">
        <UserDetails ref="step5" :data="formData" @update="updateFormData" />
      </div>

      <div class="flex justify-between mt-4">
        <button
          type="button"
          @click="prevStep"
          v-if="currentStep > 1"
          class="px-4 py-2 bg-gray-300"
        >
          Previous
        </button>
        <button
          type="button"
          @click="nextStep"
          v-if="currentStep < steps.length"
          class="px-4 py-2 bg-blue-500 text-white"
        >
          Next
        </button>
        <button
          type="button"
          @click="handleSubmit"
          v-if="currentStep === steps.length"
          class="px-4 py-2 bg-green-500 text-white"
        >
          Submit
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import Sidebar from "./components/Sidebar.vue";
import PersonalInformation from "./components/PersonalInformation.vue";
import Education from "./components/Education.vue";
import Experience from "./components/Experience.vue";
import ProfileImage from "./components/ProfileImage.vue";
import UserDetails from "./components/UserDetails.vue";

export default {
  components: {
    Sidebar,
    PersonalInformation,
    Education,
    Experience,
    ProfileImage,
    UserDetails,
  },
  data() {
    return {
      currentStep: 1,
      steps: [1, 2, 3, 4,5],
      formData: {
        firstName: "",
        lastName: "",
        email: "",
        mobileNumber: "",
        school: "",
        graduation: "",
        company: "",
        role: "",
        profileImage: null,
      },
    };
  },
  methods: {
    nextStep() {
      const stepComponent = this.$refs[`step${this.currentStep}`];
      if (stepComponent && stepComponent.validate()) {
        if (this.currentStep < this.steps.length) {
          this.currentStep++;
        }
      }
    },
    prevStep() {
      if (this.currentStep > 1) {
        this.currentStep--;
      }
    },
    goToStep(step) {
      const stepComponent = this.$refs[`step${this.currentStep}`];
      if (stepComponent && stepComponent.validate()) {
        this.currentStep = step;
      }
    },
    updateFormData(data) {
      this.formData = { ...this.formData, ...data };
    },
    handleSubmit() {
      const stepComponent = this.$refs[`step${this.currentStep}`];
      if (stepComponent && stepComponent.validate()) {
        alert("Form Submitted");
        console.log("Form Submitted", this.formData);
        (this.formData = {
          firstName: "",
          lastName: "",
          email: "",
          mobileNumber: "",
          school: "",
          graduation: "",
          company: "",
          role: "",
          profileImage: null,
        }),
          (this.currentStep = 1);
      }
    },
  },
};
</script>
<style scoped></style>
