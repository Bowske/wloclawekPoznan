<template>
  <div class="login">
    <v-facebook-login
      v-model="model"
      app-id="633593563867021"
      @sdk-init="handleSdkInit"
    ></v-facebook-login>
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
  }),
  methods: {
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
