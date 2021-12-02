<template>
  <v-app dark>
    <!--    <v-app-bar fixed app>-->
    <!--      <nuxt-link to="/">-->
    <!--        <v-toolbar-title v-text="title" />-->
    <!--      </nuxt-link>-->
    <!--      <nuxt-link to="onboarding"> 온보딩 </nuxt-link>-->
    <!--      <nuxt-link to="session"> 응원하기 </nuxt-link>-->
    <!--      <v-spacer />-->
    <!--    </v-app-bar>-->
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      title: "Woowacon",
    };
  },
};
</script>
