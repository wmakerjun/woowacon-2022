<template>
  <v-container class="h-100vh">
    <div class="view-center">
      <v-form class="onboarding-form">
        <p>이름을 입력해주세요</p>
        <v-text-field label="이름" outlined></v-text-field>
        <v-btn color="primary" depressed large class="w-100">입장</v-btn>
      </v-form>
    </div>
  </v-container>
</template>

<script>
export default {
  name: "onboarding",
};
</script>

<style scoped>
.onboarding-form {
  width: 90%;
}
</style>
