<template>
  <AppHeader @open-login-modal="isLoginOpen = true" />
  <div class="w-full flex">
    <router-view></router-view>
  </div>
  <LoginModal v-if="isLoginOpen" @close-login-modal="isLoginOpen = false"/>
</template>
// comment from sandbox2, but now is it very important

<script>
// another comment from sandbox2
import AppHeader from "./components/AppHeader";
import LoginModal from "./components/LoginModal";
import firebase from "./utilities/firebase";
export default {
  data() {
    return {
      isLoginOpen: false,
      isLoggedIn: false,
      authUser: {},
    };
  },
  mounted() {
    firebase.auth().onAuthStateChanged((user) => {
  if (user) {
    this.isLoggedIn = true;
    this.authUser = user;
  } else {
    this.isLoggedIn = false;
    this.authUser = {};
  }
});
  },
  components: {
    AppHeader,
    LoginModal,
  },
};
</script>
