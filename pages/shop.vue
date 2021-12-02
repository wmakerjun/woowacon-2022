<template>
  <v-sheet max-width="480px" height="100vh" color="#121212" class="relative">
    <div class="d-flex justify-center mt-12 mb-5">
      <nuxt-link to="/">
        <v-img max-width="150" src="/woowacon-main-logo.png" />
      </nuxt-link>
    </div>
    <div class="d-flex justify-center mt-12 mb-5">
      <v-card color="transparent" dark rounded>
        <div class="d-flex">
          <v-avatar size="75" tile>
            <v-img src="/coin2.png" />
          </v-avatar>
          <div class="d-flex align-center">
            <div>
              <v-card-subtitle class="pa-0"> 남은 포인트 </v-card-subtitle>
              <v-card-title class="text-h4 font-weight-bold pa-0"
                >{{ myPoint }}P</v-card-title
              >
            </div>
          </div>
        </div>
      </v-card>
    </div>

    <v-row justify="center" align="center" class="mx-4">
      <v-col v-for="(item, index) in items" cols="6" class="pa-2">
        <v-img :src="item.link" @click="buyItem(index)" />
      </v-col>
    </v-row>

    <v-dialog v-model="dialog" width="250">
      <v-card class="d-flex justify-center">
        <div class="pa-6">
          <v-img width="100" src="/gift.png" class="mx-auto" />
          <p class="text-center">{{ item.name }}(으)로 교환되었습니다.</p>
        </div>
      </v-card>
    </v-dialog>
  </v-sheet>
</template>

<script>
export default {
  name: "shop",
  mounted() {
    const myPoint = localStorage.getItem("myPoint");
    if (myPoint && myPoint >= 0) {
      this.myPoint = myPoint;
    } else {
      localStorage.setItem("myPoint", this.myPoint);
    }
  },
  methods: {
    buyItem(index) {
      if (this.items[index].price > this.myPoint) {
        alert(
          "금액이 부족합니다. 라이브 세션에서 응원으로 포인트를 모아보세요 🎉"
        );
        return;
      }
      this.myPoint = this.myPoint - this.items[index].price;
      this.setMyPoint();
      this.dialog = true;
      this.item = this.items[index];
      this.$confetti.start();
      this.$confetti.update({
        particles: [
          {
            type: "heart",
          },
          {
            type: "circle",
          },
        ],
        defaultColors: ["red", "pink", "#ba0000"],
      });
      setTimeout(() => {
        this.$confetti.stop();
      }, 3000);
    },
    setMyPoint() {
      localStorage.setItem("myPoint", this.myPoint);
    },
  },
  data() {
    return {
      dialog: false,
      myPoint: 1000,
      item: "",
      items: [
        {
          name: "시원한 맥주",
          link: "item1.png",
          price: 600,
        },
        {
          name: "배달이 피규어",
          link: "item2.png",
          price: 1000,
        },
        {
          name: "우아한 후드티",
          link: "item3.png",
          price: 1500,
        },
        {
          name: "배민 상품권",
          link: "item4.png",
          price: 600,
        },
      ],
    };
  },
};
</script>

<style scoped>
.v-application .text-h4 {
  font-family: hanna, "Roboto", sans-serif !important;
}
</style>
