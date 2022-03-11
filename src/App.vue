<template>
  <Profile class="profile" v-on:getId="getId" :night="night"></Profile>
  <Content class="content" :id="id" v-on:alternative="getNight"></Content>
</template>
<script>

import Content from "@/components/Content";
import Profile from "@/components/Profile";

export default {
  name: 'App',
  components: {
    Content,
    Profile
  },
  data() {
    return {
      id: null,
      night: false
    }
  },
  methods: {
    getId(id) {
      this.id = id
    },
    getNight(val) {
      this.night = val
    }
  }
}
</script>

<style>
@font-face {
  font-family: 'SF Pro Display Regular';
  src: url("./assets/font/SF-Pro-Display-Regular.otf");
}

@font-face {
  font-family: 'SF Pro Text Regular';
  src: url("./assets/font/SF-Pro-Text-Regular.otf");
}

@font-face {
  font-family: 'SF Pro Display Semibold';
  src: url("./assets/font/SF-Pro-Display-Semibold.otf");
}

@font-face {
  font-family: 'SF Pro Text Semibold';
  src: url("./assets/font/SF-Pro-Display-Semibold.otf");
}

@font-face {
  font-family: 'PingFang Regular';
  src: url('./assets/font/PingFang Regular.ttf');
}

@font-face {
  font-family: 'PingFang Bold';
  src: url('./assets/font/PingFang Bold.ttf');
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}

* {
  box-sizing: border-box;
  list-style: none;
  padding: 0;
  margin: 0;
  font-family: "PingFang Bold", "SF Pro Text Semibold", serif;
}

#app {
  width: 100vw;
  height: 100vh;
  display: flex;
}

.content {
  flex: 3 0;
  height: 100%;
}

.profile {
  flex: 1 0;
  height: 100%;
}
</style>
