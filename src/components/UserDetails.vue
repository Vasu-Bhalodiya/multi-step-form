<template>
    <div>
        <h2 class="text-xl mb-4">Form Details</h2>
        <div>
        <ul>
        <li><b>FirstName</b>{{ localData.firstName }}</li>
        <li><b>LastName</b>{{ localData.lastName }}</li>
        <li><b>Email</b>{{ localData.email }}</li>
        <li><b>MobileNumber</b>{{ localData.mobileNumber }}</li>
        <li><b>School</b>{{ localData.school }}</li>
        <li><b>Graduation</b>{{ localData.graduation }}</li>
        <li><b>Company</b>{{ localData.company }}</li>
        <li><b>Role</b>{{ localData.role }}</li>
        </ul>
        </div>
    </div>
</template>

<script>
    export default {
        props:{
            data: Object
        },
        data() {
      return {
        localData: { ...this.data },
        errors: {}
      };
    },
    methods:{
        validate() {
        if (!this.data.profileImage) {
          this.errors.profileImage = 'Profile image is required.';
          return false;
        }
        return true;
      }
    }
    }
</script>

<style scoped>

</style>