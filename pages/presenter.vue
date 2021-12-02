<template>
  <v-sheet max-width="480px" height="100vh" color="#121212" class="relative">
    <div class="d-flex justify-center align-start mt-16 w-100 h-100">
      <v-card color="transparent" elevation="0">
        <div class="d-flex justify-center">
          <v-avatar size="100">
            <v-img src="/presenter1.png" alt="presenter" />
          </v-avatar>
        </div>
        <v-card-text class="text-center">
          <div class="mb-5">
            <div class="text-h5 font-weight-bold font-hanna">조은옥</div>
            <div>DR팀</div>
          </div>
          <v-progress-circular
            :rotate="-90"
            :size="150"
            :width="15"
            :value="circleValue"
            color="primary"
          >
            <v-img width="60" src="/magic.png"></v-img>
          </v-progress-circular>
          <p class="mt-4">총 {{ circleValue * 2 }}개의 응원봉을 받았습니다!</p>
        </v-card-text>
      </v-card>
    </div>
  </v-sheet>
</template>

<script>
export default {
  name: "presenter",
  beforeDestroy() {
    clearInterval(this.interval);
  },
  mounted() {
    this.interval = setInterval(() => {
      if (this.circleValue === 100) {
        return (this.circleValue = 0);
      }
      this.circleValue += 0.5;
    }, 1000);
  },
  data() {
    return {
      interval: {},
      circleValue: 0,
    };
  },
};
</script>

<style scoped></style>
