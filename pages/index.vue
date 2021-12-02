<template>
  <div>
    <v-container class="d-flex justify-center mt-12 mb-5">
      <v-img max-width="150" src="/woowacon-main-logo.png"> </v-img>
    </v-container>

    <nuxt-link to="presenter" class="d-flex justify-center">
      <v-btn
        class="presenter-cheer-count black--text"
        rounded
        color="primary"
        small
      >
        <v-img width="15" src="/magic.png" />
        <span> 응원봉 현황 </span>
      </v-btn>
    </nuxt-link>
    <div class="carousel-container py-4">
      <client-only>
        <carousel
          :center="true"
          :autoplay="false"
          :items="2"
          :nav="false"
          :dot="false"
          :loop="true"
        >
          <div v-for="banner in activeBanners" class="ma-4">
            <nuxt-link to="session">
              <v-img :src="banner.url" />
            </nuxt-link>
          </div>
        </carousel>
      </client-only>
    </div>

    <div class="mx-5">
      <v-chip class="mb-2" color="transparent" text-color="white">
        <v-avatar left>
          <v-img src="/coin.png" width="16" />
        </v-avatar>
        응원포인트 샵
      </v-chip>
      <v-card color="#494949" dark rounded="xl">
        <div class="d-flex flex-no-wrap">
          <v-avatar class="ma-3" size="100" tile>
            <v-img src="/magic-stick.png"></v-img>
          </v-avatar>
          <div class="d-flex align-center">
            <div>
              <v-card-title class="text-h4 font-weight-bold font-hanna"
                >{{ myPoint }}P</v-card-title
              >
              <v-card-subtitle>
                응원포인트로 상품을 <br />
                교환하러 가볼까요?
              </v-card-subtitle>
            </div>
            <v-card-actions>
              <nuxt-link to="shop">
                <v-btn class="mx-2" fab dark small color="#C4C4C4" depressed>
                  <v-icon dark> mdi-arrow-right </v-icon>
                </v-btn>
              </nuxt-link>
            </v-card-actions>
          </div>
        </div>
      </v-card>
    </div>
  </div>
</template>
<script>
import { nanoid } from "nanoid";

export default {
  mounted() {
    const myPoint = localStorage.getItem("myPoint");
    if (myPoint && myPoint >= 0) {
      this.myPoint = myPoint;
    } else {
      localStorage.setItem("point", this.myPoint);
    }
  },
  data() {
    return {
      myPoint: 1000,
      item: {
        color: "#1F7087",
        src: "https://cdn.vuetifyjs.com/images/cards/foster.jpg",
        title: "Supermodel",
        artist: "Foster the People",
      },
      activeBanners: [
        {
          _id: nanoid(),
          url: "/carousel-item1.png",
          type: "Session1",
          presenter: {
            name: "조은옥",
          },
        },
        {
          _id: nanoid(),
          url: "/carousel-item2.png",
          type: "Session1",
          presenter: {
            name: "이동렬",
          },
        },
        {
          _id: nanoid(),
          url: "/carousel-item3.png",
          type: "Session1",
          presenter: {
            name: "이상은",
          },
        },
      ],
    };
  },
};
</script>

<style lang="scss">
.carousel-container {
  width: 100%;
}

.owl-dots {
  display: none;
}

.owl-stage {
  padding-top: 32px;
  padding-bottom: 40px;
}

.owl-item.active.center {
  transform: scale(1.4);
}

.v-application .text-h4 {
  font-family: hanna, "Roboto", sans-serif !important;
}

//.presenter-cheer-count {
//  position: absolute;
//  top: 0;
//}
</style>
