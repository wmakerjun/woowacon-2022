<template>
  <v-sheet max-width="480px" height="100vh" color="#2d2d2d" class="relative">
    <div class="d-flex justify-center align-center w-100 h-100">
      <v-card color="transparent" elevation="0">
        <div class="d-flex justify-center">
          <v-avatar size="100">
            <v-img src="/presenter1.png" alt="presenter" />
          </v-avatar>
        </div>
        <v-card-text class="text-center text--white">
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
            <div class="swing">
              <v-img width="60" src="/magic.png" />
            </div>
          </v-progress-circular>
          <p class="mt-5 text-white">
            총 <span class="text-h4">{{ circleValue * 2 }}</span
            >개의 응원봉을 받았습니다!
          </p>
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

<style scoped>
.text-white {
  color: white !important;
}

.swing {
  animation: swing ease-in-out 1s infinite alternate;
  transform-origin: center 40px;
  float: right;
}
.swing img {
  border: 5px solid #f8f8f8;
  display: block;
}

@keyframes swing {
  0% {
    transform: rotate(3deg);
  }
  100% {
    transform: rotate(-3deg);
  }
}
</style>
