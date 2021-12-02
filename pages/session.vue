<template>
  <v-sheet max-width="480px" height="100vh" color="#121212" class="relative">
    <iframe
      width="100%"
      height="100%"
      src="https://www.youtube.com/embed/zi5lX6Ejoh8"
      title="YouTube video player"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen
    >
    </iframe>
    <div class="d-flex justify-center">
      <div class="chat-container">
        <template v-for="message in messages">
          <v-card
            elevation="0"
            rounded="pill"
            color="rgba(0,0,0,.7)"
            class="mb-2 message-card"
          >
            <v-card-text>
              {{ message }}
            </v-card-text>
          </v-card>
          <br />
        </template>
      </div>
      <v-chip color="#ED142E" class="font-weight-bold live-chip" small
        >LIVE</v-chip
      >
      <v-text-field
        v-model="message"
        label=" 강연자분께 질문을 던져보세요"
        solo
        rounded
        filled
        class="text-input"
        :hide-details="true"
        prepend-inner-icon="mdi-emoticon-happy-outline"
      >
      </v-text-field>
      <v-btn
        @click="submitChatMessage"
        color="primary"
        class="chat-submit-button"
        small
        fab
      >
        <v-icon>mdi-arrow-up</v-icon>
      </v-btn>
    </div>
    <v-btn
      ref="cheer"
      class="font-weight-bold w-100 mt-6 cheer-up-button text-h6"
      color="primary"
      depressed
      fab
      x-large
      dark
      @click="cheerPresenter"
      >응원 <br />하기</v-btn
    >
    <div class="confetti-area"></div>
  </v-sheet>
</template>

<script>
export default {
  name: "session",
  methods: {
    cheerPresenter() {
      confetti({
        particleCount: 50,
        spread: 60,
        origin: {
          y: 0.8,
          x: 0.8,
        },
      });
    },
    submitChatMessage() {
      if (!this.message) {
        return;
      }
      if (this.messages.length > 3) {
        this.messages.splice(0, 1);
      }
      this.messages.push(this.message);
      this.message = "";
    },
  },
  data() {
    return {
      message: "",
      messages: [],
    };
  },
};
</script>

<style lang="scss" scoped>
.live-chip {
  position: absolute;
  bottom: 130px;
  left: 10%;
}

.text-input {
  position: absolute;
  bottom: 70px;
  width: 90%;
  z-index: 100;
}

.cheer-up-button {
  position: absolute;
  bottom: 140px;
  right: 6%;
  z-index: 101;
}

.confetti-area {
  position: fixed;
  bottom: 0;
  height: 300px;
  width: 80%;
}

.chat-submit-button {
  position: absolute;
  bottom: 78px;
  z-index: 101;
  right: 10%;
}

.chat-container {
  position: absolute;
  z-index: 102;
  bottom: 160px;
  left: 5%;
  max-width: 70%;
}

.message-card {
  display: inline-block;
}

.back-nav-button {
  position: fixed;
  top: 12px;
  left: 12px;
}

.cheer-up-button {
  font-family: hanna, "Roboto", sans-serif !important;
}
</style>
