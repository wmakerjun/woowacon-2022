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
    <v-chip class="my-points" color="primary">
      <v-img width="20" src="/coin.png" class="mr-1" />
      <span class="font-weight-bold">{{ myPoint }}</span>
    </v-chip>
    <v-btn
      class="presenter-cheer-count black--text"
      rounded
      color="primary"
      small
    >
      <v-img width="15" src="/magic.png" />
      <span> 응원봉 현황 </span>
    </v-btn>
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
  </v-sheet>
</template>

<script>
export default {
  name: "session",
  mounted() {
    const myPoint = localStorage.getItem("myPoint");
    if (myPoint && myPoint >= 0) {
      this.myPoint = myPoint;
    } else {
      localStorage.setItem("myPoint", this.myPoint);
    }
  },
  methods: {
    cheerPresenter() {
      confetti({
        particleCount: 50,
        spread: 60,
        origin: {
          y: 0.8,
          x: this.$vuetify.breakpoint.smAndUp ? 0.6 : 0.8,
        },
      });

      this.myPoint = Number(this.myPoint) + Math.floor(Math.random() * 10);
      this.setMyPoint();
    },
    setMyPoint() {
      localStorage.setItem("myPoint", this.myPoint);
    },
    submitChatMessage() {
      if (!this.message) {
        return;
      }
      if (this.messages.length > 2) {
        this.messages.splice(0, 1);
      }
      this.messages.push(this.message);
      this.message = "";
    },
  },
  data() {
    return {
      myPoint: 1000,
      message: "",
      messages: [],
    };
  },
};
</script>

<style lang="scss" scoped>
.live-chip {
  position: absolute;
  bottom: 140px;
  left: 7%;
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

.my-points {
  position: absolute;
  right: 6%;
  top: 48px;
}

.live-chip {
  -webkit-animation: glowing 5000ms infinite;
  -moz-animation: glowing 5000ms infinite;
  -o-animation: glowing 5000ms infinite;
  animation: glowing 5000ms infinite;
}
@-webkit-keyframes glowing {
  0% {
    background-color: #b20000;
    -webkit-box-shadow: 0 0 3px #b20000;
  }
  50% {
    background-color: #ff0000;
    -webkit-box-shadow: 0 0 40px #ff0000;
  }
  100% {
    background-color: #b20000;
    -webkit-box-shadow: 0 0 3px #b20000;
  }
}

@-moz-keyframes glowing {
  0% {
    background-color: #b20000;
    -moz-box-shadow: 0 0 3px #b20000;
  }
  50% {
    background-color: #ff0000;
    -moz-box-shadow: 0 0 40px #ff0000;
  }
  100% {
    background-color: #b20000;
    -moz-box-shadow: 0 0 3px #b20000;
  }
}

@-o-keyframes glowing {
  0% {
    background-color: #b20000;
    box-shadow: 0 0 3px #b20000;
  }
  50% {
    background-color: #ff0000;
    box-shadow: 0 0 40px #ff0000;
  }
  100% {
    background-color: #b20000;
    box-shadow: 0 0 3px #b20000;
  }
}

@keyframes glowing {
  0% {
    background-color: #b20000;
    box-shadow: 0 0 3px #b20000;
  }
  50% {
    background-color: #ff0000;
    box-shadow: 0 0 40px #ff0000;
  }
  100% {
    background-color: #b20000;
    box-shadow: 0 0 3px #b20000;
  }
}
</style>
