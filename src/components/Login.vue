<template>
  <div class="login">
    <v-facebook-login
      v-model="model"
      app-id="633593563867021"
      @sdk-init="handleSdkInit"
    ></v-facebook-login>
    <button @click="getPosts()">GET POSTS</button>
  </div>
</template>

<script>
import VFacebookLogin from "vue-facebook-login-component";

export default {
  name: "Login",
  components: {
    VFacebookLogin,
  },
  data: () => ({
    FB: {},
    model: {},
    scope: {},
    userId: null,
  }),
  methods: {
    getUserId() {
      return new Promise((resolve) => {
        this.FB.api("/me", (response) => {
          this.userId = response.id;
          resolve(this.userId);
        });
      });
    },

    getCertainGroup() {
      this.FB.api("/548739628937538", (response) => {
        console.log(response);
      });
    },

    getUserGroups(userId) {
      this.FB.api(`/${userId}/groups`, (response) => {
        console.log(response);
      });
    },
    getPosts() {
      this.getUserId().then((userId) => {
        this.getUserGroups(userId);
      });
      this.getCertainGroup();
    },
    testData(scope) {
      console.log(scope.connected);
    },
    handleSdkInit({ FB, scope }) {
      this.FB = FB;
      this.scope = scope;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
